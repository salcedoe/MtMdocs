# Multimodal Dataset of the Prostate

An exercise using 3D Slicer

## Prostate Gland

![diagram of the prostate gland][img_prostate]{width=350px}

[img_prostate]: http://res.cloudinary.com/cudenes/image/upload/v1493957481/medical_imaging/Prostate-Anatomy.jpg

The  prostate secretes the milky or white, slightly alkaline fluid, that constitutes roughly 30% of the volume of the semen.

A healthy human male prostate is classically said to be slightly larger than a walnut.

![walnut][jaw]{width=250px}

[jaw]: https://c1.staticflickr.com/5/4528/37492066184_3eb6101fee.jpg

The prostate is located immediately in front of the rectum, a few centimeters from the anus. It surrounds the urethra just below the urinary bladder.

## Ultrasound of the Prostate

### Transabdominal

In a transabdominal examination, the bladder is situated above the prostate

#### Sagittal

![Sagittal View - transducer angled caudally along midline][i_patient_sag]{width=350px}

[i_patient_sag]: http://res.cloudinary.com/cudenes/image/upload/v1493957481/medical_imaging/US_prostate_scan_plane_sag.jpg

![Sagittal view. prostate outlined by cross-hairs.][i_US_transab_sag]{width=350px}

[i_US_transab_sag]: http://res.cloudinary.com/cudenes/image/upload/v1493957481/medical_imaging/us_transabdominal_prostate-normal.jpg

#### Transverse

![Transverse View - Probe angled caudally and aligned along the transverse axis][i_patient_transverse]{width=350px}

[i_patient_transverse]: http://res.cloudinary.com/cudenes/image/upload/v1493957481/medical_imaging/US_prostate_scan_plane_ts.jpg

![Tranverse view - prostate shown here in blue][i_us_transabd_transverse]{width=350px}

[i_us_transabd_transverse]: http://res.cloudinary.com/cudenes/image/upload/v1493957481/medical_imaging/us_trasnabd_prostate_transverse_normal_hl.jpg

### Transrectal

In a transrectal examination, the bladder is below the prostate (the transducer is now closer to the prostate than it is to the bladder)

![transrectal examination][img_prostate_patient]{width=550px}

[img_prostate_patient]: http://res.cloudinary.com/cudenes/image/upload/v1493957481/medical_imaging/us_transrectal.jpg

![illustration of the view from a transrectal transducer][transrectal_illustration]{width=350px}

[transrectal_illustration]: http://res.cloudinary.com/cudenes/image/upload/v1493957481/medical_imaging/prostate_US.jpg

![screen grab of a US transrectal image][img_transrectal_US]{width=350px}

[img_transrectal_US]: http://res.cloudinary.com/cudenes/image/upload/v1493957481/medical_imaging/US_transrectal-prostate.gif

Source: [RadiologyWorld](http://www.radiologyworld.com/trans-prost.htm)

[Ultrasound images of the diseased prostate](http://www.ultrasound-images.com/prostate.htm#Imaging%20of%20the%20normal%20seminal%20vesicles,%20and%20vas%20deferens)

## MRI of Prostate

![Sagittal view of the Prostate][prostate_sagittal]

[prostate_sagittal]:https://c1.staticflickr.com/5/4485/26426042699_ac8b7f9c2b.jpg

![Transverse view  - normal exam. This view is looking up from the feet towards the head of the patient. (A: right hip, B: bladder, C: left hip, D: prostate, E: rectum)][img_mri_prostate]

[img_mri_prostate]: http://res.cloudinary.com/cudenes/image/upload/v1493957481/medical_imaging/prostate_mri.jpg

[Source](http://www.radiologyinfo.org/en/photocat/gallery3.cfm?pid=1&image=prostate-mr.jpg&pg=mr_prostate)

## Slicer 3D

### Load Sample Data

In the "Welcome to Slicer" screen, click on the "Download Sample Data" button.

Choose "Download MR-US Prostate"

### Overlay volumes

MODULE: Set View Controllers
Select "Four-Up" in the Windows View.

![][four_up]

[four_up]:https://c1.staticflickr.com/5/4491/26426040809_5a5b1fa6c4_o.png

Choose the "View Controllers" Module in the module selector.

Use the following settings:

![][view_controllers_USMRI_prostate]

[view_controllers_USMRI_prostate]:https://c1.staticflickr.com/5/4513/38170962172_bb06934cca_b.jpg

### Volumes

### Browse USProstate

1. What are the dimensions of this volume?
2. What are the dimensions of the voxels in this volume
3. Change the **LUT** of the Ultrasound to **"Magma"**
4. Where is the transducer positioned?
5. Try to locate the prostate and the bladder

### Browse MRprostate

1. What are the dimensions of the pixels in this volume
2. Change **LUT** to "**WarmShade3**"
3. Set View Control transparency to 1.0 for MRprostate
4. Find the Bladder. Hint: contrast has been added to the bladder
5. Find the prostate. Hint, look for the crescent shaped structure as seen in the [transverse view][img_mri_prostate] of the prostate in the MRI image above.
6. Find the Urethra.

### Volume Rendering

Select the Volume Rendering Module

* **Volume**: MRProstate. Turn on eye

* **Display:**

  * **Crop:** Enable. Display ROI

Crop the volume to the sagittal midline.

* What do you notice about the alignment of the MR volume to the axis

#### Slicer Scene

Slicer should now look something like this:

![slicer screengrab][prostate_MRI_US_scene]

[prostate_MRI_US_scene]:https://c1.staticflickr.com/5/4455/26426037729_22d7870b11_h.jpg

## Create Segmentations

*optional*

!!! note "Data Resolution"

    The  resolution is very low in these volumes. You will not get the prettiest segmentations.

    The prostate itself is too small and does not have enough contrast to segment using the "grow from seeds" tool. Instead, you would have to manually segment each slice of the prostate. We are not going to do that.

    The Prostate appears to be  smaller in the MR than in the US.


### Bladder

* Bring up the "Segment Editor" module
* For "Master Volume" - choose "MRProstate"

1. Add a segmentation for the bladder and call this segmentation "Bladder"
2. Use Paint to paint inside bladder
3. Add a segmentation for outside the bladder. Paint outside the bladder. Remember, you are just sampling voxels that are not bladder. You do not need a precision outline of the bladder
4. "Grow from seeds"

* Select the Bladder segmentation
* Select "Initialize"
* Scrub through the slices and look for voxels with the wrong segmentation color
* Repair any wrong segmentations using the paint brush (be sure to select the right segmentation)
* Notice that you only need to repair a small segment and the tool will update the segmentation in that region
* After you have checked all of the slices click **"Apply"**

6. "Show 3D" If you haven't done so, display the 3D view to see the result. You will probably see a large block
7. Remove Outside segmentation
8. "Smoothing"

* Use the default Kernel size
* Open
* Close
* Median

### Rectum

Repeat the same process with the Rectum

IMPORTANT DIFFERENCES

1. "Grow from seeds"

* Be sure to make the Bladder not visible (close eye next to segmentation)
* Then, under the "Masking" tab, "Editable Area", select "Outside all visible segments"

2. "Smoothing" -

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/my_ernesto/38245329261/" title="Segment Editor Grow from seeds settings"><img src="https://farm5.staticflickr.com/4497/38245329261_552a990caa_z.jpg" width="428" height="640" alt="Segment Editor Grow from seeds settings"></a>

You should get something like this:

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/my_ernesto/38245274111/" title="US MR Prostate Segment"><img src="https://farm5.staticflickr.com/4551/38245274111_2549cee58b_z.jpg" width="640" height="436" alt="US MR Prostate Segment"></a>
