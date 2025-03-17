# Workflow Overview

## Volume Review

## Preprocess data

!!! tip "ABOUT ISOTROPIC SPACING and the Spacing Scale setting"
    What isotropic spacing actually does is up- or downsample the 3D volume. Basically, you are adding or subtracting rows, columns, or slices. Subtracting rows and columns means that you are downsampling, which should ultimately create a smaller volume, which in turns saves memory (and hopefully avoids crashing Slicer). Ultimately, you want the total volume loaded into Slicer to take only 1/10 the amount of RAM that is available on your system. For 3D processing, you rarely benefit from having high in-plane resolution if distance between planes is large. For example, a volume of `2500 x 2500 x 500` (with spacing of `0.1x0.1x0.5`) will give you approximately same quality 3D reconstructions as a volume of `500 x 500 x 500` (with spacing of `0.5x0.5x0.5`). This means we rarely want to upsample and instead should use a larger Spacing scale setting to downsample the volume (even larger than shown here). See the discussion here: [Is there a way to reduce the CPU usage and reduce the amount of RAM used? - #3 by goetzf - Support - 3D Slicer Community](https://discourse.slicer.org/t/is-there-a-way-to-reduce-the-cpu-usage-and-reduce-the-amount-of-ram-used/3181/3)

## Segmentation

When you segment, you actually create a new volume that is the same size as the original volume (same number of voxels). This segmentation volume is said to mask the original volume. Segmentation volumes can be either binary volumes (true or false) or label maps, which use whole numbers to indicate connected regions. For this exercise, for example, we will create a segmentation of the Right Kidney. In this segmentation volume, all voxels pertaining to the right kidney will be labeled with a value, like 1. This is not an intensity value, but a label — that's why they are called label maps.  We will also segment the Left Kidneys — all those voxels will be labeled with a different value, like 2. And so on. Everywhere that is not segmented will have a label of 0.

**TO:DO** Diagram Showing color overlay and two volumes: one for the labelmap and one for the intensity volume

??? tip "Saving Tips and Reminders"

    **How to create Create a New Folder**. 

    Notice in the directory column that each file has a default path. We want to change the folder paths for all of these files so that they are stored in the same new folder. To do so, do the following:

    - Ensure that all of the files are checked. 
    - Click on the "Change directory for selected files" 
    - In the dialog the pops-up, navigate to the location where you want to create your folder. The Documents folder is a good place to start (Macs should avoid saving stuff on the desktop as it can slow down your computer.).
    - Create a new folder in that location
    - Call this folder "CTFemur" or something similar. And select OK. 

    **Save everything**

    - Every file should now have the same path in the directory column 
    - Every file should be checked in the check column.
    - Click on the Save Button. 
  
Here is a video overview of the Grow from Seeds method: [PERKlab - Grow from seeds](https://www.youtube.com/watch?v=8Nbi1Co2rhY)

## Model Creation

## Export
