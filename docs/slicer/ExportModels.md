
#### Export to OBJ

An OBJ file is a surface model file format.

In this step, we are going to export a surface model of the brain and the two tumors as a single obj file. There are other surface model file types, but OBJ is one of the most universal. 

You create an OBJ file by the following steps.

1. Switch to the Segmentations Module (![][img-segmentations])

2. Set the **Active segmentation** to "MRTumorModels segmentation" node that you just created

    >You should see your three segmentations in the table:
    >
    >![][img-seg-models]

3. In the **Export to files** section, use the following settings

![][img-MR-tumor-export-to-merged-obj-settings]

[img-MR-tumor-export-to-merged-obj-settings]:https://saldenest.s3.amazonaws.com/slicer/MR-tumor-export-to-merged-obj-settings.png width=400px

[img-MR-tumors-merged-segs-panel]:https://saldenest.s3.amazonaws.com/slicer/MR-tumors-merged-segs-panel.png width=400px

>- Be sure to set the appropriate Destination folder
>- Be sure to click on "merge into single file"

[img-seg-models]:https://saldenest.s3-us-west-2.amazonaws.com/slicer/MRTumors-segmentations-models.png width=400px

SAVE YOUR WORK!

---

## Challenge

How would you create this?

![][img-MR-tumors-cropped-render-with-segs]



### Volume Rendering with Tumors

1. Turn on Tumor Segmentations in 3D view
2. Turn on coronal slice view in 3D
2. Render the Stripped Skull volume
3. Crop the volume along the interhemispheric fissure
4. Make sure your tumor model is visible




[img-MR-tumors-cropped-render-with-segs]:https://saldenest.s3.amazonaws.com/slicer/MR-tumors-cropped-render-with-segs.png 


    
