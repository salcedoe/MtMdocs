# Volume Segmentation

Volume segmentation is exactly like [Image Segmentation](../imageProcessing/ImageSegmentation.md), but in 3D: instead of just segmenting neighboring pixels, you also segment voxels from adjacent image slices.

The process of segmentation in 3D allows you to isolate specific anatomical structures or features within medical images, such as organs, tumors, or blood vessels, by identifying and labeling voxels that belong to each region of interest. This process is essential for quantitative analysis, visualization, and further processing tasks.

Many of the functions we used for 2D Images work for 3D volumes, include the thresholding and morphological operation functions. There are also many 

Volume segmentation is the process of partitioning a 3D volume into distinct regions or structures based on characteristics such as intensity, texture, or spatial properties. In MATLAB, segmentation tools  MATLAB provides both automated segmentation functions (like active contours and region growing) and interactive tools (such as the Volume Segmenter app) that let you manually refine segmentation results. Once a structure is segmented, you can measure its volume, create 3D surface models for visualization, or use it as a mask for further analysis.

## Example: Embedded Shapes

We start with a simple volume, 'shapes3D.mat'(1).
{ .annotate }

1. The volume, 'shapes3D.mat' is stored as a MATLAB .mat file and can be found in the Unit 3 data folder.

```matlab linenums="1" title="Load Vol"
clearvars
mmSetUnitDataFolder(3) % switch to the Unit 3 Folder
load('shapes3D.mat','Vol'); % load volume as Vol
```

`Vol` is a `318x318x159` uint8 volume.  We can render the volume using the Volume Viewer App.  

```matlab linenums="1" "Volume Render"
volumeViewer(Vol)
```

![Volume render of multiple 3D shapes](images/volumeViewer-3D-shapes.png){ width="750"}
>**Volume Render of volume containing multiple 3D shapes.** Here we use the volumeViewer app to render the volume using the Cinematic Rendering setting and the "hot" colormap. As you can see in the 3-D volume panel, there are for four embedded shapes in the volume: a Cylinder , a Diamond, a Cube, and a Sphere. Each shape comprise a  uniform set of intensity values, which is why each shape is rendered in a different hot pseudocolor in the 3D view and in differing shades of gray in the cross-sectional orthogonal views. Intensity values  of 64, 128, 192, and 250.  This is the

 to signify the varying intensity values of the shapes. The shades of gray in the orthogonal views indicate the same thing  You can see these intensity values by 