# Course Functions

!!! note "Preface"
    
    All MtM course functions are prefaced with `mm`.

## Image Processing

### mmGetWatershed

Performs the necessary steps for a watershed transformation of a mask. Based on this [MATLAB blog](http://blogs.mathworks.com/steve/2013/11/19/watershed-transform-question-from-tech-support/)

![watershed example](images/mmGetWatershed_example.png){ width="450"}

**INPUTS**

- **BW**:  logical array (2D or 3D)
- **PixSz**: Pixel Size of the extended regional minima inside the blobs being separated. The smaller the value, the smaller the extended regional minima - see imextendedmin
**Optional**

- **conn**: connectivity  - see imextendedmin
- **ShowSteps**: boolean - display watershed steps

**Output**

- **BW**: Watershed transformed Mask

```matlab linenums="1" title="Examples" 
BW = mmGetWatershed(BW,5);
BW = mmGetWatershed(BW,5,ShowSteps=true); % displays transformation steps
BW = mmGetWatershed(BW,5,8); % pixel size 5, connectivity 8
BW = mmGetWatershed(BW,[5 3 1]);  % runs the watershed 3 times with 3 different pixel sizes
```

### mmGetTextureFilters

Apply texture filters to input image. Texture filters include standard deviation, range, and entropy.

![texture filters of ferret image](images/mmGetTextureFilters_ferret.png){ width="450"}
> Text Filters applied to an image of a Ferret and displayed using mmShowStruct

 **INPUTS**

- **p**: a structure that must contain a field called either 'rgb' or 'img'. `rgb` should be an rgb image. `img` should be a grayscale image.
  
- **nhood**: (optional) a neighborhood matrix (typically logical or array of ones).

 **OUTPUT**

- **p**: updated structure containing four new fields: gray, std, rng, and ent

```matlab linenums="1" title="Examples" 
p = mmGetTextureFilters(p) % get filtered images with default neighborhood

% Apply a 7x7 neighborhood and display all filtered images
p = mmGetTextureFilters(p,true(7)) % get filtered images with a neighborhood of 7x7
mmShowStruct(p) % display filtered images
```

### mmReadImgND

This function uses the [MATLAB Bio-formats toolbox](https://www.openmicroscopy.org/bio-formats/downloads/) to read in multidimensional image stacks.

 **INPUTS** (optional)

- file_path is a path to an image file. If you don't input a file path, you will be prompted for a path.

 **OUTPUTS**

- **IMGND**: an XYZCT multidimensional array
- [IMGND, metadata] = mmReadImgND(file_path): the metadata from the array in XML format

```matlab linenums="1" title="Example" 
[IMGND, metadata] = mmReadImgND(file_path)
```


## Plotting Functions

### mmShowHist

Tiles an image with its histogram in one figure. Image is display above the histogram (two row tiles per image). Corrects MATLAB inexplicable inability to pair `nexttile` with `imhist` by using `subplot` for tiling.

![example of Grayscale image](images/mmShowHist_MOB.png){ width="150"}

If you input an RGB image, this function will automatically index out the channels and display the histogram for each channel.

![example color image](images/mmShowHist_color.png){ width="250"}

**INPUTS**

Required:

- **img**: an image matrix

Optional:

- **col** (default = 1): current column position 
- **num_cols** (default = 1): total number of columns in the figure.
- **title_str** (default = empty): a string to title the image
- **add_color** (logical = false): if true add color

```matlab linenums="1" title="Examples" 
mmShowHist(img) — displays image above its histogram
mmShowHist(img, 2, 6) - displays the image and the histogram in the 2nd
column of a six-column figure
```

### mmShowBurnImage

Wrapper for `imoverlay` but with syntax similar to `imshowpair`. Simplifies creating a burned image, where a masked is burned into an image

![img-name](images/mmShowBurnImage_strawberries.png){ width="250"}

**INPUTS**

- **img**: a grayscale or rgb image
- **mask**: a binary mask

**OPTIONS**
- **color**: the color of the burned image (default = yellow)

```matlab linenums="1" title="Examples" 
mmShowBurn(rgb,mask)
mmShowBurn(rgb,mask,color='white')
```

### mmShowStruct

Displays in a single figure images that are packaged in a structure

INPUTS
- **S**: a structure contain fields with image variables
- **fn2display**: cell array or string contain the names of the fields you
want to display
- **titles** (optional): string array of titles for plots

```matlab linenums="1" title="Examples" 
mmShowStruct(p)
mmShowStruct(p,fn2display={'rgb','gray'})
mmShowStruct(p,fn2display={'rgb','gray'},titles={'Original','Grayscale'})
```

### mmBoxSwarm

A wrapper for `swarmchart` and `boxchart` that overlays a swarm chart on a box chart.

![img-name](images/swarm-box-Y.png){ width="150"} ![img-name](images/swarm-box-XY.png){ width="350"}

**Inputs**

- **x**: (*Optional*) Enter empty brackets to generate a series of ones
- **y**: Vector of Numeric ata

**Options**

- **PlotType**: enter 'violin' for a violin plot (default is 'swarm')
- **XAxVisible**: display x-axis (default = 'off')
- **MarkerFaceColor**: set marker face color
- **MarkerFaceAlpha**: set marker face alpha (default =0.25)
- **doBoxPlot**: overlay boxplot (default is true)
- **BoxFaceColor**: set boxplot face color
- **BoxFaceAlpha**: set boxplot face alpha (default = 0.1)
- **Notch**: Turn on box plot notch (default =  'off')
- **XJitterWidth** set jitter width of swarm chart (default = 1)

```matlab linenums="1" title="Examples" 
mmBoxSwarm([],nD.data); % y-data only
mmBoxSwarm(x,y,'BoxFaceColor','k','Notch','on','MarkerFaceAlpha',0.15) % grouping data and y-data
```

### mmAddScaleBar

Adds a scalebar to current image

**INPUTS**

- **ax**: the handle to the axis where you want to add your scale bar
- **width**: the length of the scalebar 
- **widthPERpixel**: the dimensions of a pixel side (e.g. um per pixel)

**OPTIONAL INPUTS**

- **Color**: the color of the scale bar
- **Line Thickness**: thickness of the scale bar (in points)
- **pos**: a row vector containing the X and Y coordinates where
        you want the scale bar. You can enter empty brackets to skip
- **unit**: a character array indicating the unit of measure. If
        inputted, the width of the scalebar will be printed above the bar

```matlab linenums="1" title="Examples"
add_scale_bar(gca,100, 2.3);
add_scale_bar(gca,50,0.23,'white', 4, [],'µm');
```

NOTE: the measurements don't have to be in microns. They just have
be consistent between `width` and `widthPERpixel`

## 3D Slicer Functions

Functions to import medical volumes created in 3D Slicer

### mmGetSlicerSegTable

Returns a table containing the properties (e.g. name, color, etc.) of the segmentations found in a seg.nrrd file

- **Input**: file path to a segmentation file
  
- **Output**: a table with segmentation names, layer, label, and color values

```matlab linenums="1" title="Example" 
segT = mmGetSlicerSegTable(seg_file_path)
```

### mmGetAllSlicerSegTables

Loads the metadata and Segmentation Properties from all Slicer segmentation files found in the same folder

**Input**

- **filePath:** file path to the folder containing segmentation files (`*.seg.nrrd`)

**Output**

- **T**: Slicer Segmentation table. Contains information (name, color) about segmentations created in Slicer Segment Editor module
- **contentT**: Table containingg information about the segmentation files

```matlab linenums="1" title="Example" 
[segT,contentT] = mmGetAllSlicerSegTables(fullfile(paths.folder, paths.fileWC))
```

### mmGetMedicalVolumeSegment

Simplifies indexing out a segment from a Slicer Segmentation volume. The function returns a structure that contains the mask of the indicated segment, color, and transformation matrix of the selected segmentation. First load a Slicer Segmentation file using `medicalVolume` and the Slicer segmentation table using `mmGetSegTable`.

**INPUTS**

- **mV**   (required):    medicalVolume of a Slicer Segmentation dataset
- **segT** (required):    table - table created by mmGetSlicerSegTable
- **segName** (optional): string - Name of Segment to return.

If segName not provided, the function prompts for a segmentation to be
selected from the inputted segT table

**OUTPUTS**

**S**: The function retunrs a structure with the following fields

- **segName**: Name of selected segment
- **mask**: binary mask of the selected segment
- **color**: color of the segmentation as set in Slicer
- **tform**: transformation matrix to properly orient segmentation
- **spacing**: Voxel spacing
- **volume**: calculated using `regionprops3`.

### mmPlotAllSeg

Wrapper function that plots all segmentations from a 3D Slicer segmentation volume. Options include Smoothing and decimation, and lighting.

 **INPUTS**:

- **Vol**: 3D array
- **segT**: Table containing the following slicer info — Name, Layer, LabelValue, Color

 **OPTIONAL INPUTS**. Enter empty brackets if skipping.

- **new_figure**: logical (default = true). Create new figure if true
- **falpha**: scalar (0-1, default = 0.5) - transparency of the faces
- **smooth**: boolean (default=false). True means Smooth volume
- **affTrfm**: 4X4 3D affinity transformation matrix (default = [], no transformation). Used to transform the vertices to match the orientation and size of the original volume.

**OUTPUT**

- **hp**: array of patch handles to surface plots

```matlab linenums="1" title="Examples" 
hp = mmPlotAllSeg(Vol,segT);
hp = mmPlotAllSeg(Vol,segT, falpha=0.25, affTrfm=tform);

tform = createScaling3d(Sseg.xyz)
segT = mmGetSlicerSegNames(seg_file)
hp = mmPlotAllSeg(Vol,segT,affTrfm=tform);
```

## Surface Functions

Functions to process and manipulate surface meshes. Many of these functions work well with the vertices field in a patch handle, allowing for real-time update of the surface plot. 

### mmPlotMask2Surface

Wrapper function that creates an isosurface from an input volume. Options include Smoothing of Volume and decimation, and lighting.  Default plots surface as a patch in one simple function call.
  
**INPUTS**

- **BW**: logical 3D array

**Optional Inputs** (in this order). Enter empty brackets if skipping.

- **fcolor**: character array (default = 'cyan') - facecolor of the
          isosurface.
- **falpha**: scalar (0-1, default = 0.5) - transparency of the faces 
- **lightEMup**: boolean (default = true) - add lights to plot. Set to
          false for multiple function calls (and then set to true 
          on the final call). Otherwise you'll add too many lights
          to scene
- **report**: boolean (default=false) - print a report of settings to command window
- **smooth**:    boolean (default=false). True means Smooth volume
- **decimator**: decimation factor (0-1, default=0.15) of the generated surface 
- **affTrfm**:   4X4 3D affinity transformation matrix (default = [], no transformation)
          Used to transform the vertices to match the orientation and size of the  
          original volume. Requires matGEOM - plugged into
          transformPoint3d

**OUTPUT**

- hp: handle to patch

```matlab
hp = mmPlotMask2Surface(BW);
hp = mmPlotMask2Surface(BW,fcolor='cyan');
hp = mmPlotMask2Surface(BW,fcolor='magenta',falpha=0.25, lightEMup=true, decimator=0.2);

tform = createScaling3d(Sseg.xyz)
hp = mmPlotMask2Surface(BW,'magenta',transform_mat=tform); 
```

### mmGetSurface

Generate a surface mesh of the inputted 3D volume.  Returns a face-vertices structure. 

**INPUTS**

- **Vol**: a 3D volume
- **iv** (numeric): isovalue from which to generate the surface
- **decimator** (0-1): amount by which to decimate the generated surface. 
- **use_fast_march** (logical): Use the function `extractIsosurface` to more quickly generate an isosurface. Default = true

**OUTPUT**

- **fv**: a faces-vertices structure
- **s**: string reporting the decimation

```matlab linenums="1" title="Examples" 
fv = mmGetSurface(Vol);
fv = mmGetSurface(Vol,0.5,0.1) 
```

REQUIREMENTS:
Medical toolbox required for fast marching isosurface

### mmPlotSurface

Wrapper function to `patch`. plots the input fv structure as a patch. Lights not added. Use
`mmSetSurfacePlotProps` to add lighting and correct aspect ratios

**INPUTS**

- **fv**: a faces-vertices structure (output from isosurface)
- **fcolor**: face color
- **falpha**: face alpha

**OUTPUT**

- **hp**: handle to the patch

```matlab linenums="1" title="Example" 
hp = plot_surface(fv,'cyan',0.5)
mmSetSurfacePlotProps % add lighting to plot
```

### mmAlignSurface2Axes

Transforms the vertices so that the direction of most variance is aligned to the x-axis. Based on this [discussion](https://www.mathworks.com/matlabcentral/answers/66051-how-do-i-move-a-cloud-of-points-in-3d-so-that-they-are-centered-along-the-x-axis).

**INPUT**:

- **Vert**:  NX3 array of Vertices to be transformed

**OUTPUTs**

- **Vert**: Transformed vertices
- **Vd**: Variance
  
```matlab linenums="1" title="Example"
hp.vertices = mmAlignSurface2Axes(hp.vertices)
```

### mmRotateSurfaceVertices

Rotate the vertices of a surface around the specified axis by the specified angle (in degrees).

**INPUTS**

- **vertices**: (matrix): Nx3 vertices
- **ax** (character array): axis around which to rotate — x, y, or z
- **angl** (scalar): angle (in degrees) to rotate
- **centerVerts** (logical): optional. Center Vertices around 0,0,0 prior to rotation

```matlab linenums="1" title="Example" 
vertices = mmRotateSurfaceVertices(vertices, 'x',45)
```

### mmAlignSurfaces

Registers two point clouds using an iterative closest point algorithm. This function requires the **Computer Vision Toolbox**. The inputs and outputs of this function are a matrix of 3D coordinate points (xyz)

**Inputs**

- **SurfFixed**: NX3 vertices matrix of Fixed Surface
- **Surf2Move**: NX3 vertices matrix of Surface to be moved (registered to fixed surface)

**Output**

- **Surf2Move**: NX3 vertices matrix of registered surface

```matlab linenums="1" title="Example" 
 [vertMoving,rmse] = mmAlignSurfaces(vertFixed, vertMoving,options)
```

### mmCalcSurfaceAreaFromMesh

This function will calculate the sum of all triangles in the mesh to calculate Surface area.

If P1, P2, and P3 are 3D coordinate vectors of the three respective vertices of some particular triangle, then its area is given by:

```matlab linenums="1"
AreaP1P2P3 = 1/2*norm(cross(P2-P1,P3-P1));
```

> Adapted from [this discussion](https://www.mathworks.com/matlabcentral/answers/271797-surface-area-of-a-3d-surface)

```matlab
[SurfaceArea] = mmCalcSurfaceAreaFromMesh(Vertices,Faces)
```

## Apps

### mmSliceView

A custom image stack viewer app. Can handle 3D and 4D image stacks. Can load Image Stacks and accompanying binary Masks

#### Benefits

- Relatively Responsive
- Quickly scrub through image using the mouse scroll wheel
- Turn on image contrast for each slice
- Simultaneously load an image stack and a mask — overlay the mask on each slice view

```matlab
mmSliceView(STACK)
```

<!-- ![screen grab of mmSliceView app](../imageProcessing/images/mmSliceView-screengrab.png){ width="450"} -->

## Utility Functions

### mmSetFigPublication

Sets the default axes font to 16 and figure color to white

```matlab linenums="1" title="Example" 
mmSetFigPublication(14) % Set Font size to 14
```

### mmSetUnitDataFolder

Sets the current folder to the indicated unit data folder from the [MtMdata Shared Folder] (https://drive.mathworks.com/sharing/36f2e302-384d-4c4e-aa98-8e853c1051c0)(Must be at root level of MATLAB drive)

```matlab
mmSetUnitDataFolder(3) % sets folder to unit 3 
```

### mmGetChannelMap

This function returns a color map (with 256 shades) of the indicated color 

**Input**: a channel name, letter, or index
**Output**: a colormap of the shade indicated by the input

```matlab linenums="1" title="Example" 
red_cm = mmGetChannelMap('red')
green_cm = mmGetChannelMap('g')
```