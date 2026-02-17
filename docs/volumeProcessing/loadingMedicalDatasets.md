# Loading Medical Datasets

To load medical datasets into MATLAB, we will load them as [medicalVolume](https://www.mathworks.com/help/medical-imaging/ref/medicalvolume.html){target="_blank"} objects (1).
{ .annotate}

1. Requires the [Medical Imaging Toolbox](https://www.mathworks.com/products/medical-imaging.html).

!!! note "What are medicalVolume objects anyway?"

    A medicalVolume is a variable class that packages together the Voxel information (i.e., the volume), the metadata, and the Volume Geometry, which can transform the volume into [Anatomical Coordinate Space](https://slicer.readthedocs.io/en/latest/user_guide/coordinate_systems.html) (e.g. LPS). Although it looks like a `structure`, a medicalVolume is an `object`, which is a variable class that combines data (properties) with functions and methods.  As such, there are defined ways to modify any of its fields, and you can't, for example, simply add a new field to an mV object using dot notation. But not to worry—we will be using medicalVolume objects primarily as read-only variables and we won't really mess with modifying any of its fields. 

## Loading DICOM Datasets

DICOM Datasets are organized as a series of images in folders. For this example, we will use the DICOM data found in the `unit3/MedicalVolumeDICOMData` folder.

```
MedicalVolumeDICOMData/
├── LungCT01
│   ├── CT000000.dcm
│   ├── CT000001.dcm
│   ├── CT000002.dcm
|   ⋮
│   └── CT000087.dcm
├── LungCT02
│   ├── CT000000.dcm
│   ├── CT000001.dcm
│   ├── CT000002.dcm
|   ⋮
│   └── CT000175.dcm
└── LungCT03
    ├── CT000000.dcm
    ├── CT000001.dcm
    ├── CT000002.dcm
    ⋮
    └── CT000087.dcm
```

>The MedicalVolumeDICOMData folder contains three Lung CT Datasets: LungCT01, LungCT02, and LungCT03. In each of these folders are a series of DICOM images (.dcm files) that comprise the dataset. The LungCT02 dataset is larger, containing 176 images, whereas the other two datasets only contain 88 images each.

MATLAB has many functions and apps that can handle DICOM datasets. **`dicominfo`** loads the DICOM metadata. Every single image in a DICOM volume contains the metadata for the entire volume, so here we input the first image from the LungCT02 folder.

```matlab linenums="1" title="Load DICOM Metadata"
mmSetUnitDataFolder(3); % change Current Folder to the Unit 3 Data Folder
meta = dicominfo(fullfile("MedicalVolumeDICOMData","LungCT02","CT000000.dcm")) % path to the first DICOM image in the LungCT02 dataset
```

```matlab
 meta = struct with fields:
                             Filename: '/Users/ernesto/MATLAB-Drive/MtMresources/MtMdata/unit3/MedicalVolumeDICOMData/LungCT02/CT000000.dcm'
                          FileModDate: '18-Apr-2022 18:04:00'
                             FileSize: 256798
                               Format: 'DICOM'
                        FormatVersion: 3
                                Width: 512
                               Height: 512
                             BitDepth: 16
                            ColorType: 'grayscale'
       FileMetaInformationGroupLength: 212
           FileMetaInformationVersion: [2×1 uint8]
              MediaStorageSOPClassUID: '1.2.840.10008.5.1.4.1.1.2'
           MediaStorageSOPInstanceUID: '1.3.6.1.4.1.9590.100.1.2.286066201332069648426726334394087096117'
                    TransferSyntaxUID: '1.2.840.10008.1.2.4.70'
               ImplementationClassUID: '1.3.6.1.4.1.9590.100.1.3.100.9.4'
            ImplementationVersionName: 'MATLAB IPT 9.4'

```

>**`dicominfo`** returns a structure (`meta`) containing the DICOM metadata.

The DICOM Browser can be used to browse individual image slices in a DICOM dataset.

```matlab linenums="1" title="Bring up the DICOM browser" 
 dicomBrowser("MedicalVolumeDICOMData") % input the folder containing the DICOM datasets
```

![dicom browser](images/dicom-browser-lungs.png){ width="750"}

>The DICOM Browser displays some metadata and the image slices. Click on the row in the "Studies" panel (top) to bring up a list of the datasets (called "series") in the "Series" panel (bottom). Notice that the series are named not by their folder name, but by the "SeriesDescription" found in the metadata. Click on one row of the series table to bring up the series images in the "Series Viewer" panel (right). By scrubbing up and down you can view all the images in a given series.

A DICOM dataset can be loaded into the MATLAB workspace as a `medicalVolume`. Here we load the data from the `LungCT02` folder ("Lung 30%").

```matlab linenums="1" title="Load DICOM as a medicalVolume"
 mV = medicalVolume("MedicalVolumeDICOMData/LungCT02") % input DICOM folder
```

```matlab
 mV = 
  medicalVolume with properties:

                  Voxels: [512×512×176 int16]
          VolumeGeometry: [1×1 medicalref3d]
            SpatialUnits: "mm"
             Orientation: "transverse"
            VoxelSpacing: [0.76172 0.76172 1.25]
            NormalVector: [0 0 1]
        NumCoronalSlices: 512
       NumSagittalSlices: 512
     NumTransverseSlices: 176
            PlaneMapping: ["sagittal"    "coronal"    "transverse"]
    DataDimensionMeaning: ["left"    "posterior"    "superior"]
                Modality: "CT"
           WindowCenters: [176×1 double]
            WindowWidths: [176×1 double]
```

## Loading 3D Slicer Datasets

3D Slicer files usually end with the `.nrrd` extension (1). You can load these files into MATLAB as a `medicalVolume`. In this example, we load the [CT Angiogram dataset](../slicer/CTACardioSegment.md) found in the `unit3/CTACardio` folder.
{ .annotate }

1. That's right. It's a "NERD" file. Read all about it in the [3D Slicer documentation](https://slicer.readthedocs.io/en/latest/user_guide/data_loading_and_saving.html#supported-data-formats).

```matlab linenums="1" title="Load Slicer Intensity Volume"
mmSetUnitDataFolder(3); % change folder to the Unit 3 Data Folder
mV = medicalVolume("CTACardio/CTACardio Crop.nrrd") % note the .nrrd extension
```

In addition to loading the volume itself (Voxels field), you also get metadata (all the other fields).
```matlab  
mV = 

  medicalVolume with properties:

                  Voxels: [465×276×390 int16]
          VolumeGeometry: [1×1 medicalref3d]
            SpatialUnits: "unknown"
             Orientation: "transverse"
            VoxelSpacing: [1.027 1.027 1.027]
            NormalVector: [0 0 1]
        NumCoronalSlices: 276
       NumSagittalSlices: 465
     NumTransverseSlices: 390
            PlaneMapping: ["sagittal"    "coronal"    "transverse"]
    DataDimensionMeaning: ["right"    "anterior"    "superior"]
                Modality: "unknown"
           WindowCenters: []
            WindowWidths: []
```

As you can see, the dimensions of the intensity volume are `465×276×390` and is a signed integer 16-bit. This means there can be negative values in the volume to accommodate the Hounsfield units found in CT datasets.

Slicer segmentation files end with the `.seg.nrrd` extension. We can also load Slicer Segmentation Volumes as medicalVolumes:

```matlab linenums="1" title="Load Segmentation Volume"
mmSetUnitDataFolder(3);
segFile = fullfile('CTACardio', 'Salcedo segmentation.seg.nrrd') % .seg.nrrd extension
segMV = medicalVolume(segFile) % load as medical volume
```

!!! warning "Missing Endian Values"
    
    You may get a warning of a 'Missing 'endian' value in the file metadata'. Don't worry, this warning is safe to ignore. If you want to force MATLAB to ignore the warning, you can use the following syntax prior to loading the Segmentation Volume:

    ```matlab
    warning('off', 'medical:medicalVolume:noEndian')
    ```
    

```matlab title="Segmentation Volume loaded as a medicalVolume" 
 segMV = 

  medicalVolume with properties:

                  Voxels: [465×276×390 uint8]
          VolumeGeometry: [1×1 medicalref3d]
            SpatialUnits: "unknown"
             Orientation: "transverse"
            VoxelSpacing: [1.027 1.027 1.027]
            NormalVector: [0 0 1]
        NumCoronalSlices: 276
       NumSagittalSlices: 465
     NumTransverseSlices: 390
            PlaneMapping: ["sagittal"    "coronal"    "transverse"]
    DataDimensionMeaning: ["right"    "anterior"    "superior"]
                Modality: "unknown"
           WindowCenters: []
            WindowWidths: []
```

Notice that the Segmentation volume has the same dimensions as the intensity volume, but is unsigned 8-bit.  And, instead of intensity values, these volumes contain labels (unsigned whole numbers) that signify the segmented internal structures.

While a `medicalVolume` object contains information critical to processing and visualizing the volume, it lacks the properties set in Slicer, like label values, names, and colors. To load these properties, you can use the course function **`mmGetSlicerSegmentInfo`**.

```matlab linenums="1" title="Load Segmentation Metadata"
segT = mmGetSlicerSegmentInfo(segFile) % input path to a .seg.nrrd file
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

`mmGetSlicerMetadata` returns a table containing the Slicer properties, with columns for segmentation name, layer, label value, and color.  As you can see, this segmentation volume has three segmentations: 'right kidney', 'left kidney', and 'aorta' labeled by the values `1`, `2`, and `3`. So in the entire volume, there are only four different values: `0-3`, where `0` means no segmentation. The Color column contains the color of each segmentation, as it was set in 3D Slicer.

!!! note "What is a Layer?"

    In the Slicer metadata, there is a column for layer. In this example, the value is the same for all segmentations (1) and the segmentation volume is 3D. In other volumes, the layer values can differ, if "overlaying segments" was enabled in Slicer. Overlaying segments allows you to have more then one segment in the same physical space, like Total Lung and Right Lung, where the right side of Total Lung and Right Lung are virtually identical.  So, if there is more than one layer value, then the segmentation volume is 4D, not 3D, and "Layer" indicates the index value in the 4th dimension.  You would index in the 4th dimension to access these separate segmentations. 
    
