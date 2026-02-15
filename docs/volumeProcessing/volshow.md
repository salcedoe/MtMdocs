# volshow

The function **volshow** can display Medical Volumes directly in live scripts. It's a simpler and faster way to display volumes without launching a separate app like the Medical Volume Viewer.

```matlab linenums="1" title="Display Medical Volume using volshow"
mmSetUnitDataFolder(3) % cd to unit3 folder
intMV = medicalVolume("CTACardio/CTACardio Crop.nrrd") % load intensity volume as a medicalVolume
volshow(intMV)
```

![volshow ctacardio](images/volshow-ctacardio-crop.png){ width="450"}
>Volume render of the CTACardio CT volume

By default, **`volshow`** creates a 3D viewer with a blue background and a black gradient. Also notice that medicalVolumes are transformed into Anatomical Space (LPS). 

You can right-click on the `volshow` window to bring up a contextual menu with additional options, such as displaying a scale bar or voxel info.

![volshow contextual menu](images/volshow-contextual-menu.png){ width="250"}
>If you uncheck "Always embed Viewer in Live Editor", volshow will display the volume in a separate figure.

## Adjusting display

If you want to modify the background of the figure, you first need to create an empty scene using **`viewer3D`**. Here we create a viewer with a white background and no gradient.

```matlab linenums="1" title="White Background"
hvr = viewer3d(parent=uifigure,BackgroundColor="white",BackgroundGradient="off",CameraZoom=1); % set background color to white and turn off gradient
hvs = volshow(intMV,parent=hvr);
```

![volshow ctacardio crop white background](images/volshow-ctacardio-crop-whitebackground.png){ width="450"}

You can adjust the rendering style by modifying the `RenderingStyle` field in the `volshow` handle:

```matlab linenums="1" title="Change Rendering Style to GradientOpacity"
hvs.RenderingStyle = "GradientOpacity"; % volshow handle
hvs.GradientOpacityValue = .1; % additional setting for Gradient Opacity
```

![comparison of volshow rendering styles](images/volshow-rendering-comparisons.png){ width="450"}
>Comparison of Rendering Styles using `volshow`

We can also modify the Colormap and add a title by modifying the respective fields in the volshow and viewer3d handles, respectively:

```matlab linenums="1" title="Change colormap and add title"
hvs.Colormap = parula; % volshow handle
hvr.Title = "CTACardio" % viewer3D handle
```

![volshow with parula colormap and title](images/volshow-ctacardio-crop-parula-title.png){ width="450"}

## `mmSetVolShowColors`

`mmSetVolShowColors` is a utility function for **`volshow`** that simplifies the customization of the display. It automatically changes the background color of the `volshow` background to white and then applies a Medical alphamap and colormap to the volume render. The alpha- and colormaps are the same options available in the [Medical Volume Viewer](medVolumeViewer.md)

To use, first display a volume using `volshow` and then simply input the handle from `volshow` into `mmSetVolShowColors`.

```matlab linenums="1" title="Apply CT Bone "
hvs = volshow(intMV);
mapName = mmSetVolShowColors(hvs)
```

The function displays a list dialog with a choice of alphamap presets.

![mmSetVolShowColors list dialog](images/mmSetVolShowColors-dialog.png){ width="150"}

Select an alphamap to apply.

![lung alpha map](images/mmSetVolShowColors-lung.png){ width="450"}
>Here we apply the lung alphamap and colormap.

## Overlaying label maps

Label Maps (or segmentation volumes) can be added as an overlay to the volume rendering using the following syntax.

```matlab linenums="1" title="Overlay Render"
segMV = medicalVolume("CTACardio/Salcedo Segmentation.seg.nrrd"); % load volume

hvs = volshow(intMV,... % intensity volume is the first input
    OverlayData=segMV.Voxels, ... % add label map as Overlay data
    RenderingStyle="GradientOpacity", ... % change rendering style
    OverlayAlpha=0.4); % adjust overlay transparency 
hvs.Parent.BackgroundGradient = 'off';
hvs.Parent.BackgroundColor = 'white';
```

 Notice that "OverlayData" must be inputted as an array (not a medical volume), which is why we input the 'Voxels' field at the second input.

![ctacardio with kidneys](images/volshow-ctacardio-kidney-overlay.png){ width="250"}
>**Overlay Render**. Kidney (orange and yellow) and Aorta (purple) segmentations overlaid on a volume render of the CTA Cardio CT volume

```matlab linenums="1" title="SlicePlane Render"
hvr = viewer3d(parent=uifigure,BackgroundColor="white",BackgroundGradient="off",CameraZoom=1); % set background color to white and turn off gradient
volshow(segMV,parent= hvr,RenderingStyle="Isosurface",Colormap=hot) % display total segmentation as slice planes
volshow(intMV,parent= hvr,RenderingStyle="SlicePlanes",OverlayData=segMV.Voxels) % display total segmentation as slice planes
```

Here we first create a viewer window (`viewer3d`), then we have two calls to `volshow`, with both calls using the same viewer window as the parent. In the first call, we render the label volume as an "Isosurface". This gives the render that blocky label map appearance. We use a Colormap setting of "hot" to make the segments appear red. In the second call to `volshow`, we render the intensity volume as orthogonal slice planes. We also add the label map as overlay data. This adds color to the orthogonal slices where the label overlaps with the intensity volume. The second `volshow` call must be the SlicePlanes render, so you can interactively manipulate the position of the orthogonal planes.

![slice plane](images/volshow-ctacardio-kidney-overlay-sliceplanes.png){ width="450"}
>**SlicePlane Render**. Segments rendered in red. Intensity volume rendered as orthogonal planes

You can click and drag on the orthogonal planes to move their position.
