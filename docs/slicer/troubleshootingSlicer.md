# Troubleshooting Slicer

Slicer can be a bit cantankerous at times. So be sure to save your data, often. Also, avoid removing, moving, or renaming slicer files (e.g. .NRRD files) outside of Slicer.

## Restart

If Slicer is not acting as expected, the first thing to try is to quit and restart Slicer.  

## Load without the scene file

If you still are having strange issues, especially with segmentation:

1. Close the scene so no data is loaded in Slicer (or simply restart Slicer)
2. Reload the data without the scene file (the .MRML file)

!!! abstract "Loading a project without the scene file"

    1. Click on the `Add Data` button in the Slicer toolbar or from the Slicer menu to bring up the "Add data into the scene" dialog
    2. In the dialog, click the "Choose Directory to Add" button
    3. Navigate to your Slicer project folder
    4. Click "Open"

    You should now see a list of the Slicer project folder contents:

    ![Screenshot of Slicer project folder contents selection dialog](images/slicer_troubleshoot_ChooseDirToAdd.png){ width="750"}

    - Uncheck any scene (.mrml) or image (.png) files, as these are not needed for loading the raw data.
    - Uncheck any Surface model files (e.g .mtl and .obj), as you don't need to load those back into Slicer
    - Once you have finished unchecking the unnecessary files, click `OK`.

Your data should now be loaded. You may not see what you last saved, but you should have all the relevant data and should be able to segment or proceed with any other steps you were previously taking.

Note, the next time you save your work, Slicer will automatically generate a new Scene file (.mrml). Be sure to use the lasted scene file when reopening your work. 