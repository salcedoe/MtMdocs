# Medical Volume File Formats

There are two main types of file formats for Medical Volumes

1. **Raster Files** - stores the data as a grid of voxels (just like 2D raster formats tiff or png)
2. **Geometry Definition Format files** - stores 3D model data as a list of vertices and faces (and other data)

## Volume (Raster) Formats

A raster format is a file format used to store the voxel intensity data (like a 3D image file). We will use several different common formats, as detailed below.

!!! abstract "A selection of Raster Formats"

    | Format    | File Extension    | Read    | Write    |
    | :-------------    | :--------------------    | :----  | :----  |
    | DICOM    | .dcm    | yes    | no    |
    | NRRD    | .nrrd, .nhdr    | yes    | yes     |
    | VTK    |.vtk    |yes    |yes     |
    | NifTI    |.nia, .nii, .nii.gz    |yes    |yes     |
    | PNG    |.png    |yes    |yes     |
    | TIFF    |.tif, .tiff    |yes    |yes     |

    You can find a complete list of the 3D slicer supported files on the [Supported Formats Page](https://slicer.readthedocs.io/en/latest/user_guide/data_loading_and_saving.html)

### DICOM

**Digital Imaging and Communications in Medicine.** DICOM is one of the main standards for handling, storing, printing, and transmitting information in medical imaging. It includes a file format definition and a network communications protocol.

Image stacks are typically saved as individual image files. The metadata in each image file contains information about the entire image stack.

The [DICOM standard](http://dicom.nema.org/standard.html) is maintained by the Medical Imaging & Technology Alliance, which is part of National Electrical Manufacturers Association - the people that build CT and MRI scanners

### NRRD

![nrrd logo][img_nrrd]{width=100px}

[img_nrrd]: http://teem.sourceforge.net/img/nrrd256.jpg 

[nrrd](http://teem.sourceforge.net/nrrd/) ("nearly raw raster data") is a library and file format for the representation and processing of n-dimensional raster data used by 3D Slicer.

It is intended to support scientific visualization and image processing applications.

NRRD datasets are typically stored as a single file.

### VTK

![vtk logo][img_vtk]{width=100px}

[img_vtk]:http://www.vtk.org/files/logos/VTK-logo-medium-res.jpg 

The [Visualization Toolkit](http://www.vtk.org) (VTK) is an open-source, freely available software system for 3D computer graphics, image processing and visualization.

Open source software that uses VTK is usually pretty powerful. For example, 3D Slicer uses VTK for visualization.

VTK has its own file format. 

### NIfTI

 ![nifti logo][img_nifti]{width=100px}

[img_nifti]: http://nifti.nimh.nih.gov/iconBlue.jpg 

[Neuroimaging Informatics Technology Initiative](http://nifti.nimh.nih.gov/). An NIH funded initiative to support and enhance the use of informatics tools related to neuroimaging.

## 3D Geometry Model Formats

!!! abstract "3D Slicer Supported Geometry file formats"

    | Format | Extension | Read | Write|
    | :--- | :----: | :----:| :---:|  
    |VTK Polygonal Data    |.vtk    |yes    |yes    |
    |VTK XML Polygonal Data    |.vtp    |yes    |yes    |
    |STL    |.stl    |yes    |yes    |
    |OBJ    |.obj    |yes    |depends    |  

    *Note: Write support for OBJ files may depend on the software used. Some tools can export OBJ files, while others may not.*

### STL

[STL (STereoLithography)](http://www.wikiwand.com/en/STL_(file_format)) - originated from stereolithography CAD software created by 3D Systems.

An STL file describes a raw unstructured triangulated surface by the unit normal and vertices (ordered by the right-hand rule) of the triangles using a three-dimensional Cartesian coordinate system.

STL coordinates can be positive or negative numbers; the format does not specify units or scale, and the units are arbitrary.

### OBJ

[OBJ](http://www.wikiwand.com/en/Wavefront_.obj_file) (or .OBJ) is a geometry definition file format developed by Wavefront Technologies for its Advanced Visualizer animation package

A very simple file format that represents 3D geometry and can store the following info:

- The position of each vertex

- The UV position of each texture coordinate vertex

- The vertex normals

- The faces that make each polygon defined as a list of vertices

- The texture vertices, which define how textures are mapped onto the surface of the model.

## Additional Slicer Specific Formats

- **MRB:** Medical record bundle. Can group different Slicer supported files together into a single, unified file. e.g. In an MRB, you can store both Raster Volumes and Models together.
