# Medical Segmentation Surface Rendering

## Slicer Segmentation Files

To render a segmentation from a 3D Slicer segmentation volume, we need to first load the volume as a `medicalVolume`

```matlab linenums="1" title="Load Segmentation Volume"
mmSetUnitDataFolder(3);
segFile = fullfile('CTACardio', 'CTACardio Crop segmentation.seg.nrrd')
segMV = medicalVolume(segFile)
```
We also need to load the metadata

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

There are three different segmentations in this volume.

## Render all Segments

We can render all segmentations in a segmentation volume using the course function **`mmPlotAllSeg`**:

```matlab linenums="1" title="Plot all Segmentations"
figure;
mmPlotAllSeg(segMV,segT) 
```

![surface render of kidneys and aorta](images/mmPlotAllSeg-kidneys.png){ width="250"}
>Surface render of kidneys and aorta using colors set in Slicer. The default transparency is set to 0.5.

## Render a Selected Segment

If you want to specify the segment to render, first index out the segment from the segmentation volume and then render.

The function `mmGetMedicalVolumeSegment` indexes out the indicated segment and returns some basic metadata on the segment as `struct`.

```matlab linenums="1" title="Get Segment"
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

>mmGetMedicalVolumeSegment returns a structure. The specified segment is returned as a logical array that can be found in the 'mask' field.

You can then render the segment using `mmPlotMask2Surface`.

```matlab linenums="1"
hp = mmPlotMask2Surface(segS.mask,fcolor=segS.color,transform=segS.tform);
title("Right Kidney")
```

>`hp` is a handle to the surface render. Notice that we input the transformation matrix, `tform`, to properly transform the segmentation in real-world space (millimeter space). 

![img-name](images/surface-render-right-kidney.png){ width="250"}

## Rendering using the Medical Toolbox

You can surface render using the Medical Toolbox, as follows

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
>The render is a little more blocky then the `mmPlotMask2Surface` render, but includes the tools included with `volshow`.