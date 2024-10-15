## Todo:

- Double check the Import feature 
- 9553F is all screwed up with the last version (5.2.1) — maybe change the folder that is imported?
- Current solution is to remove the files from the s60 folder: I1-I400 (basically anything below I1000)
- Reimport
- Click on the center volume button (in volumes module) to fix
- Add a new section that shows how to save the data as NRRD files (maybe)
- NEW ANGLE: load a trouble-free dataset vs a troubled one


## DICOM 

DICOM is one of the main standards for handling, storing, printing, and transmitting information in medical imaging. In a DICOM dataset, the image stacks are typically saved as individual image files. Each image contains the metadata for the entire stack.

DICOMs are notoriously difficult to work with. In this module, we will learn to work with them

{{TOC}}

## Objectives

- Learn about the DICOM file format
- Learn how to segment a femur from the cadaver dataset series
- Learn how to separate fused segmentations (ie femur head from pelvis)


## CT DICOM Dataset

This [zip file](https://saldenest.s3.amazonaws.com/anat6205_resources/UNIT_3/9553F.zip) contains a DICOM dataset from one of the cadaver scans.

For those of you who are zip-adverse, here is the MATLAB code to have MATLAB unzip it for you:

```matlab
zipfile = websave('9553F.zip','https://saldenest.s3.amazonaws.com/anat6205_resources/UNIT_3/9553F.zip')
unzip(zipfile)
```
 
After you have downloaded the zip file and extracted the contents, you should have a folder called 9553F. 

Inside this folder are four more folders:

- S30
- S40
- S50
- S60

And inside each of these folders are the actual DICOM image files. 

* I20
* I30
* I40
* I50
* I60
* I70
* I80
* I90
* ...


Notice the unhelpful names and lack of file extensions. It is difficult to sort out what volumes are contained in this dataset. For the record, there are 4 different volumes.

### Import dataset into slicer

#### DICOM Database

Slicer includes a DICOM database. This database contains a repository of information specific to the image files in a DICOM dataset. This database helps load frequently accessed datasets quickly. Every time you load a DICOM dataset, the location of this dataset is stored in the database. 

SO, first, move the folder you just downloaded to a location on your computer where you want to keep it (at least through December). If you move the location of this folder after import, Slicer may not be able to find the data and you will have to reimport. 

Next, bring up the DICOM dataset browser by clicking on this icon:

![][load_dcm]

Click on the **Import DICOM files** button.

![<p></p>][img-dicom-button]

[img-dicom-button]:https://saldenest.s3.amazonaws.com/slicer/import-dicom-button.png width=200px

Browse your computer and select the uncompressed, uzipped 9553F folder that you just downloaded. 

Your DICOM browser window should now have some data, like this: 

![][dicom_browser_ct_9553F]

Notice there are multiple, semi-hierarchal fields:
- The **top** field lists the studies that have been imported. In this case, we have one study: 9553F. This is actually a dataset from a CT scan of one the cadavers from 2016. 
- The **middle** field contains information about the selected study in the top field
- The **bottom** field contains the volumes in the study. In this case there are 4 volumes
	- HEAD
	- HEAD BONE
	- BODY
	- BODY BONE

To inspect the metadata, right-click on Body to bring up the contextual menu...

![<p></p>][img-dicom-context-menu]

[img-dicom-context-menu]:https://saldenest.s3.amazonaws.com/slicer/dicom-metadata-contextual-menu.png width=200px

and select "View DICOM metadata"

Scroll to down "ImageComments" and you will see that this metadata is specific to "Head"

![][dicom-metadata-ct-9553F]

Notice the:

- Scroll bar at the top: There are 159 different images, so 159 different metadata headers. Most of the metadata is the same, except for a few image specific fields
- Tag Names: (0008, 0005)? These are the weird DICOM specifications. Double-click on one of the tags to bring up a website explaining the tag. 
- Values:
	- Modality: CT
	- AcquisitionData: 2016
	- Manufacturer: Philips (this is for the CT machine)
	- ManufacturerMOdelName: Gemini TF TOF 64 (The model name: The imager looks something like [this](https://www.philips.co.in/healthcare/product/HC882476/gemini-tf-big-bore-pet-ct-scanner). It is also capable of performing PET)
	- Institution Name: CTRIC ([Colorado Translational Research Imaging Center](http://www.ucdenver.edu/academics/colleges/medicalschool/departments/Radiology/Research/ctric/Pages/CTRIC.aspx) - this CT was scanned here on campus)
	- ScanType: Helix (the method of scanning used on the cadaver - see lecture on CT)

And there is lots more metadata to browser through, a lot of which is incomprehensible. 


[dicom-metadata-ct-9553F]: https://saldenest.s3.amazonaws.com/slicer/dicom-metadata-ct-9553F.png
[dicom_browser_ct_9553F]:https://saldenest.s3.amazonaws.com/slicer/dicom_browser_ct_9553F.png

[load_dcm]: https://saldenest.s3.amazonaws.com/slicer/dicom-load-button.png width=70px


## Load Dataset

To load the dataset, select the name of the volume in the lower field. In this example, load "BODY BONE". Note, you can select more than one volume.  Only select "BODY BONE". 









 
