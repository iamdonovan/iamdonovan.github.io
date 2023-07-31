mapping glacier area change
===========================

.. note::

    This practical was written for use in ArcMap 10.* - the tool names should be broadly similar in ArcGIS Pro.


data and setting up
-------------------

Create a folder in your home directory called **glacier_mapping**. Inside of this folder, create another folder called
**temp_files**. As we go through the steps of this exercise, we’ll be creating lots of files, and it’s a good idea to
keep things organized. Copy the provided Landsat scenes into your glacier mapping folder, and start Arcmap.

Now, load the provided Landsat images into a new Arcmap document. For now, we’ll stick with looking at the Red, NIR,
and SWIR bands. For the Landsat 5 scene (**LT52080041990232KIS00**), this means loading bands 3, 4, and 5. For the
Landsat 8 scene (LC82080042014218LGN00), this means loading bands 4, 5, and 6. We have cropped these scenes to only
include a small area of interest, which should help them load faster, and also decrease the amount of work needed when
manually correcting glacier outlines.

Go ahead and save the map document, giving it an appropriate name.

When we start to manually edit the glacier outlines, it will be helpful to have a color image to look at. Using the
**Composite Bands** tool, create a color composite of bands 3, 2, and 1. Make sure to put the bands in the correct
(descending) order. Save the output to your glacier_mapping folder as **LT52080041990232KIS00_B321.tif**.

.. note::

    Remember that when choosing your own images, you want to ensure that you choose scenes from the same time of year,
    usually later in the year - this helps minimize the amount of snow in the scene, which decreases the likelihood of
    mapping seasonal snow cover in addition to glaciers. When attempting to calculate glacier area changes, we want to
    make sure that enough time has passed between images so that we can actually detect a signal. Typically, 5-10 years
    is considered sufficient separation for most glaciers.

band ratios and thresholding
-----------------------------

We’ll start by creating a two band ratios, first a ratio of the Red/SWIR, and second the NIR/SWIR. To do this, we use
the **Raster Calculator** tool. Open the tool, and insert the expression below into the box:

.. code-block:: text

    Float("LT52080041990232KIS00_B3.TIF") / "LT52080041990232KIS00_B5.TIF"

Save the raster to your temporary folder, calling it **ratio_tm3_tm5.tif**. Repeat these steps for the NIR/SWIR bands,
this time calling the output **ratio_tm4_tm5.tif**.

.. card::
    :class-header: question
    :class-card: question

    :far:`circle-question` Question
    ^^^

    Look at the two ratio images, and see if you can see any differences between them. What seems like an appropriate
    threshold to use for the TM3/TM5 ratio?

To actually use the threshold to mask the image, we again use the **Raster Calculator** tool. Enter the following
formula into the box, replacing ``threshold`` with your chosen value:

.. code-block:: text

    Con("ratio_tm3_tm5.tif" > threshold, 1, "")

Save the result as **mask1.tif** in your temporary folder. This formula tells the tool to create a new raster.
Everywhere the *condition* is met (i.e., everywhere the TM3/TM5 ratio is greater than the threshold), we’ll have a 1;
everywhere the condition is not met, we have a ``NoData`` value.

Inspect the resulting raster. This looks pretty good, though we’ve managed to get a lot of water caught up in our mask.
We can fix this by imposing a second threshold on TM Band 1 (blue), making sure that only pixels with a value above a
second threshold are considered. Open the **Raster Calculator** tool again, and enter this formula, saving the result
to **mask2.tif** in your temporary folder:

.. code-block:: text

    Con( ("ratio_tm3_tm5.tif" > threshold) & ("LT52080041990232KIS00_B1.TIF" > 65), 1, "")

This time, the result should look much cleaner. We have still mapped quite a lot of snow fields around the glacier,
but we no longer have so much water included in the mask. We’ll get rid of these in a little bit, once we’ve created a
polygon shapefile of our mask.

creating glacier outlines
--------------------------

To create a polygon shapefile from our mask raster, open the **Raster to Polygon** tool. Use your second mask raster
as the input, and save the output to the temporary folder as **initial_mask.shp**. Uncheck the **simplify polgyons**
box. We should now have polygon outlines of our mask, including both the glacier and the snowfields along the side.

The easiest way to get rid of all of the small snowfields is to calculate the area of each feature, then select features
based on a minimum area, and create a new layer based on that selection.

To calculate the area, we must first add a field to the layer. Open the attribute table for the layer, and under
options, select **Add Field**. Call the field **Area**, make sure it is of type ``Float``, and give it a precision of
15 and a scale of 2. Now, right-click on the newly added field, and select **Calculate Geometry**. Don’t worry for now
about the warning message. Select **Area**, and make sure the units are **square meters**. Click **OK**.

We want to make sure we only have the largest polygons, so let’s first sort the area to see where we might see a clear
break in the data, and then we’ll select the data by attributes to create a new layer. It looks like a clear break is
around 400,000 m:sup:`2` (or ∼450 pixels), but you are welcome to try a different area threshold.

Using the **Select by Area** tool (one of the buttons in the attribute table), enter ``"Area" > 400000`` in the box.
Then, right-click on the layer in the table of contents, and select **Selection** >
**Create Layer from Selected Features**. Export the new layer as a new shapefile called **initial_glacier_mask.shp**
to your temporary folder (right-click, **Data** > **Export Data**).

cleaning up the outlines
-------------------------

Great! Now we have glacier outlines from 1990. But, if you look at them, they’re a bit incomplete and messy, and they
don’t cover everything we want them to cover ("the debris problem"). This means that we have to manually edit the layer,
removing any areas that look like they might not be glacier (see example below in Fig. 1a,b).

Create a copy of your **initial_glacier_mask** layer. In the **ArcCatalog** tab, navigate to your temporary folder.
Right-click on **initial_glacier_mask.shp** and select **Copy**, then right-click on the temporary folder and select
**paste**. Rename this file **final_glacier_mask.shp**, and load it into your map document. Now we can edit this layer,
and later compare the results to our original glacier mask.

In addition to the color composite image, we can also use the thermal band, which gives us an idea of the surface
temperature. Load this band (TM band 6). Note that the units are not actually temperature, although we could convert
this band to temperature values, provided that we knew the emissivity of the surface (generally speaking, 0,9 is an
okay first estimate for water, snow, and and ice). We can clearly see that the glacier is much, much cooler
than the surrounding rock and vegetation (and water).

Using the color and thermal rasters to guide you, clean up the outlines, removing any false snowfields, and including
any areas that you think are debris-covered glacier. When you have finished, go ahead and re-calculate the area of the
feature(s) in your layer, save the results, and stop editing.

.. note::

    Note: at this stage, we have a glacier complex, that is not separated into individual glacier
    outlines (such as the RGI data is). Unfortunately, this next step can be a bit more complicated,
    but some excellent articles on the subject are , or .

area changes
-------------

Now that we have a glacier outline and area from 1990, we can use more recent outlines to see how much glaciers on
Barentsøya have changed over the past 25+ years. Load the **Barentsøya_rgi50.shp** file, and move it so that it is
above your glacier mask in the table of contents. To get a more quantitative idea of how much change has happened, we
can use the **Symmetrical Difference** tool.

Our **input feature** is your final, edited, 1990 glacier mask. The **update feature** is the RGI outline. We have
merged the outlines from the RGI, so that we can compare with our glacier mask directly. Save the output to the
temporary folder as **glacier_changes.shp**, and open the attribute table when the tool finishes processing.

The table can be a bit confusing to understand, but for our purposes we’re only really interested in the ``FID_final``
(or similar). This indicates the features that existed in the 1990 glacier outline, that don’t exist in the updated
version (and vice-versa).

You should see two features, one with an FID of **0**, and another with and FID of **-1**. The -1 indicates areas that
were not in the 1990 outline, but were in the updated outline (i.e., areas where the glaciers have advanced, or where
we made a mistake in our 1990 outline). Similarly, the **0** indicates areas covered by the 1990 outline that aren’t
covered by the updated outline (i.e., the glaciers have retreated.)

Let’s go ahead and change how this layer displays, so that we can more easily see the changes. In the **Symbology** tab
of the properties window for this layer, select **Categories** > **Unique Values**. Make sure the **FID_final** field
is selected, and add all values. Rename the labels to reflect the type of change (i.e., glacier advance/retreat), and
choose appropriate colors. Change the label heading to **Change Type**, and de-select **all other values**. Now, when
we make a map legend with our data, we can more easily understand what the different symbols mean.

Make a map of the glacier changes, with an appropriate background image (i.e., your 1990 color composite image). Include
the updated glacier outlines, and make sure the layers are slightly transparent (so that we can also see the background
image). Add a legend and scale bar, and any other features you think are appropriate.

further work
-------------

If you have time, go ahead and repeat the steps of creating a glacier outline, this time using the Landsat 8 data.
Remember that the bands have different numbers (refer to the lecture notes or ask if you don’t remember which ones
correspond to which TM bands). You should also be able to calculate the total glacier change as a percentage, as well
as the total advance and retreat (as an area). Ask around if you are not sure how to do this.
