# Loading Medical Datasets into MATLAB

To load medical datasets into MATLAB, we will use functions from the [Medical Imaging Toolbox](https://www.mathworks.com/products/medical-imaging.html). Primarily, we will load datasets as [medicalVolume](https://www.mathworks.com/help/medical-imaging/ref/medicalvolume.html) objects.

!!! note "A word on medicalVolume objects"

    A medicalVolume is a variable class that packages together the Voxel information, metadata, and Volume Geometry. The Volume Geometry can be used to transform the volume into [Anatomical Coordinate Space](https://slicer.readthedocs.io/en/latest/user_guide/coordinate_systems.html) (e.g. LPS). Although it presents as a structure, a medicalVolume is an object, which is a variable class that combines data (properties) with functions and methods.  As such, there defined ways to modify any of its fields, and you can't, for example, simply add a new field to an mV object using dot notation. But not to worry—we will be using medicalVolume objects primarily as read-only variables and we won't really mess with modifying any of its fields. 

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

The 3D Slicer default is to save volumetric data as NRRD files (1). These files end either with a `.nrrd` extension for volumetric data or `.seg.nrrd` extension for Segmentation data.
{ .annotate }

1. Refer to the [3D Slicer documentation](https://slicer.readthedocs.io/en/latest/user_guide/data_loading_and_saving.html#supported-data-formats) for more information on supported data files.

You can load NRRD files into MATLAB as a `medicalVolume`. In this example, we load the [CT Angiogram dataset](../slicer/CTACardioSegment.md) found in the `unit3/CTACardio` folder.

```matlab linenums="1" title="Load a NRRD File"
mmSetUnitDataFolder(3); % change folder to the Unit 3 Data Folder
mV = medicalVolume("CTACardio/CTACardio Crop.nrrd")
```

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

>As you can see, the dimensions of the intensity volume 465×276×390. The volume is a signed integer 16-bit to accommodate the intensity Hounsfield units.

We can similarly load a Slicer Segmentation Volume:

```matlab
 mV = medicalVolume("CTACardio/CTACardio Crop segmentation.seg.nrrd")
```

```matlab
 mV = 

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
```

>The Segmentation volume has the same dimensions as the Intensity volume, but its bit class is unsigned 8-bit to accommodate the small number of labels found in the segmentation volume.

While a medicalVolume object of a Slicer Segmentation volume contains information critical to processing and visualizing the volume, it lacks the Segment properties such as label values, names, and colors. The course function **`mmGetSlicerSegmentInfo`** loads these segment properties and formats the information into a table.

```matlab linenums="1" title="Load Segment Properties"
segT = mmGetSlicerMetadata("CTACardio/Salcedo Segmentation.seg.nrrd") % input path to a .seg.nrrd file
```

```matlab
segT =

  3×4 table

       SegName        Layer    LabelValue                Color            
    ______________    _____    __________    _____________________________

    "right kidney"      1          1         0.56471    0.93333    0.56471
    "left kidney"       1          2               0    0.59216    0.80784
    "aorta"             1          3         0.84706    0.39608     0.3098
```

>The `segT` table contains the properties set in the Slicer Segment editor, such as Segmentation Name and Color. It also list the LabelValue and Layer of each segment. Segment Layer is equivalent to a 4D index. Overlaying segments, such as the Kidney Medulla inside a Kidney segmentation, are stored in different layers of the volume (So, you need to index the 4th dimension to access these different layers).
