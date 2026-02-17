# Surface Rendering Medical Segmentations

To render a segmentation as a 3D surface, we need to:

1. Load the Segmentation volume (e.g. a `.seg.nrrd` file) into MATLAB
2. Create a 3D surface from one of the segmentations in that volume.
3. Render the 3D surface

## Slicer Segmentation Files

In this example,  we [load a Slicer segmentation volume as a medicalVolume](loadingMedicalDatasets.md).

```matlab linenums="1" title="Load Segmentation Volume"
mmSetUnitDataFolder(3);
segFile = fullfile('CTACardio', 'CTACardio Crop segmentation.seg.nrrd')
segMV = medicalVolume(segFile)
```

We also load the metadata from the volume.

```matlab linenums="1" title="Load Segmentation Metadata"
segT = mmGetSlicerSegmentInfo(segFile)
```

```matlab title="Segmentation Metadata"
segT =

  3×4 table

       SegName        Layer    LabelValue                Color            
    ______________    _____    __________    _____________________________

    "right kidney"      1          1         0.56471    0.93333    0.56471
    "left kidney"       1          2               0    0.59216    0.80784
    "aorta"             1          3         0.84706    0.39608     0.3098
```

As you can see, there are three different segmentations in this volume.

## Render a Selected Segment

If you want to specify the segment to render, you must first index out the segment from the segmentation volume and then render it. The function `mmGetMedicalVolumeSegment` simplifies this process:

```matlab linenums="1" title="Get right kidney Segment"
segS = mmGetMedicalVolumeSegment(segMV,segT,segName='right kidney') 
```

```matlab
segS = 

  struct with fields:

    segName: 'right kidney'
       mask: [465×276×390 logical]
      color: [0.56471 0.93333 0.56471]
      tform: [1×1 affinetform3d]
    spacing: [1.027 1.027 1.027]
     volume: 99574
```

`mmGetMedicalVolumeSegment` returns a structure that includes a logical mask of the specified segmentation ('right kidney' field) and some basic metadata on the segment.

Now we have the segmentation we want as its own volume (segS.mask). Next, we need to create a surface from this volume (using `isosurface`). And then render the surface (using `patch`). The course function `mmPlotMask2Surface` performs both of these steps in one function call.

```matlab linenums="1" title="Render Kidney Surface" 
hp = mmPlotMask2Surface(segS.mask,fcolor=segS.color,transform=segS.tform);
title("Right Kidney")
```

>mmPlotMask2Surface returns a handle to the surface render (`hp`). Notice here we input the mask of the kidney (`segS.mask`) as the first input. We also input the transformation matrix, `tform`, as the third input. This  properly transforms the segmentation into anatomical space (millimeter space).

![img-name](images/surface-render-right-kidney.png){ width="250"}

## Rendering using the Medical Toolbox

You can also render a segment using the Medical Toolbox, as follows:

```matlab
hvr = viewer3d("BackgroundColor",'white','BackgroundGradient','off'); % create viewer
surf1 = images.ui.graphics.Surface(hvr,... % viewer handle
    Color=segS.color, ... % face color of render
    Data=segS.mask, ... % input mask
    Alpha = 0.75, ... % set transparency
    Wireframe="off",... % turn off wirefram
    Transformation=segS.tform); % transform into real world space
```

![surface render of right kidney](images/medToolBox-surface-render-right-kidney.png){ width="350"}
>In this example, the function `images.ui.graphics.Surface` creates the surface and renders in one step. The resulting render is a little more blocky then the `mmPlotMask2Surface` render, but can be more easily combined with [`volshow` visualization methods.](volshow.md)

## Render all Segments

We can render all segmentations in a segmentation volume with one function call using the course function **`mmPlotAllSeg`**:

```matlab linenums="1" title="Plot all Segmentations"
figure;
mmPlotAllSeg(segMV,segT) 
```

>The `mmPlotAllSeg` uses the `isosurface` function to create the 3D Surface and then the `patch` function to render the surface. For volumes with more than one segmentation, it repeats the process for each segmentation. As you can see below, we get one surface render for each segmentation in the volume

![surface render of kidneys and aorta](images/mmPlotAllSeg-kidneys.png){ width="250"}
>Surface render of kidneys and aorta using colors set in Slicer. The default transparency is set to 0.5.
