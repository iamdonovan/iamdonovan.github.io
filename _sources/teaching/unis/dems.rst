dem differencing and geodetic mass balance
===========================================

.. note::

    This practical was written for use in ArcMap 10.* - the tool names should be broadly similar in ArcGIS Pro.

data and setting up
--------------------

Create a folder in your home directory called **dem_differencing**. Inside of this folder, create another folder called
**temp_files**. As we go through the steps of this exercise, we'll be creating lots of files, and it's a good idea to
keep things organized.

Copy the provided DEMs, stable ground mask (**stable_ground.tif**), glacier outlines (**Sabine_Land_RGI50.shp**), and
Excel spreadsheet (**DEM_Co-Registration_Tool.xls**) to your home directory. Start Arcmap.

Today, we'll return to our excursion area of Tunabreen and Von Postbreen. Load in the two DEMs provided, the stable
ground mask, and the glacier outlines. Save the map document to your DEM differencing folder, using an appropriate name.

differencing without co-registration
-------------------------------------

First off, we’ll difference the two DEMs without first co-registering them, just to see the errors that can be
introduced by using un-registered DEMs. We also will use this information to calculate the offsets in the two datasets.
Open the **Raster Calculator**, and insert the following formula into the box:

.. code-block:: text

    "ArcticDEM_Svalbard.tif" - "S0_1990_DTM_ND.tif"

Save the results to your temporary folder, calling it **initialDH.tif**. Change the color scheme to something a bit
easier to interpret, and look at the results. You should notice a pattern in the difference map similar to what we saw
in lecture - the shifts in the DEM cause apparent elevation changes on stable ground. Our aim is to remove these errors
by co-registering the DEMs so that they more accurately line up.

co-registration
----------------

To co-register the DEMs, we have to generate a slope and aspect raster for the primary DEM (**ArcticDEM_Svalbard.tif**).
Do this, saving the results to your temporary folder.

Now, we want to select a random sample of 5000 points from each of these rasters, to calculate the offsets. But, we
want to ensure that we only select off-glacier points for our analysis. Open the **Create Spatially Balanced Points**
tool, which allows us to generate a set of sample points. For the **inclusion probability raster**, choose
**stable_ground.tif**, and for the number of output points, choose 5000. Save the results to your temporary folder as
**sample_points.shp**.

Now that you have a set of point locations, we have to get the slope, aspect, and initial elevation difference values
at each point. Open the **Extract Multi Values to Points** tool. Choose **sample_points.shp** as your
**input point features**, and for the input rasters, choose your initialDH, slope, and aspect rasters (in that order),
and rename the output fields names for each raster to be ``initialDH``, ``slope``, and ``aspect``.

Select **bilinear interpolation of values at point locations**, and click **OK**.

Open the attribute table for your sample points. You should see three new fields: ``initialDH``, ``slope``, and
``aspect``. We could input these data directly to the co-registration algorithm, but chances are that we have a lot of
low-slope areas, which will make finding our offsets more difficult. Let’s remove these points by using the
**Select by Attributes** tool, then inputting the following formula to the box:

.. code-block:: text

    "slope" > 7

This will select all points with a slope greater than 7 degrees. Save this selection as a new layer, and export the
attribute table to your temporary folder as a dBASE table called **initial_sample_points.dbf**.

Open this table in MS Excel. Open the DEM co-registration tool, too (the excel spreadsheet we provided).

In order to use the DEM co-registration tool, we first have to install the **Solver** add-on to Excel. To do this,
click **File** > **Options** > **Add-Ins**. Next, make sure that **Excel Add-ins** is selected at the very bottom of
the panel, and click **Go...**. Select **Solver Add-in**, and click **OK**.

Next, we want to copy and paste the data we exported into the appropriate columns in the co-registration tool
(red columns). Make sure that the number of entries in the black columns matches the red columns, pasting/removing
entries as needed. Finally, at the top of the spreadsheet, make sure that the co-registration parameters ``a``, ``b``,
and ``c`` are set to an initial value of 1.

Click on the **Data** tab, then the **Solver** button. Make sure that ``C6`` is set as the **Objective** if it isn’t
already, select **min**, and make sure that **by changing variable cells** is set to ``$C$3:$C$5``.

Click **Solve**. If everything has gone well, you should see new values in the **Output** fields. If all did not go
well, stop and ask the instructor for help.

Now that we have an initial estimate for the offset between the DEMs, we can shift the secondary DEM. In Arcmap, open
the **Shift (Data Management)** tool. Select the secondary DEM (**S0_1990_DTM_ND.tif**) as the input raster.

Use the ∆x, ∆y values given by the DEM co-registration tool, and save the output as **S0_1990_DTM_shift1.tif**.

In the **Raster Caclulator**, difference the original, primary DEM (**ArcticDEM_Svalbard.tif**) with this shifted DEM,
making sure to also subtract the ∆z value output by the co-registration tool.

You should now see less of a pattern off of the glacier areas, but there may still be some differences - it can take a
few iterations to find a good solution to the co-registration. If you are satisfied with the DEM, go ahead and stop
here, but feel free to continue refining the co-registration.

geodetic mass balances
------------------------

Once you are satisfied that your DEMs are co-registered properly, we can calculate the geodetic mass balance for each
of the glaciers in our study area. To do this, we use the **Zonal Statistics as Table** tool.

The **input raster or feature zone data** should be the RGI outlines. The **Zone Field** is ``RGIID``, and the
**input value raster** is your final, co-registered DEM difference raster. Output the table to your temporary files
folder, select **ALL** as the **statistics mean**, and click **OK**.

Open the resulting table and look at the results. Note that the **sum** is not actually in the units of volume
change - to get this, we need to multiply the **SUM** field by the square of the DEM pixel
size. To do this, add a field to the table, call it **Vol_Chg**, and make it a float with a precision of 15 and a
scale of 2.

Right-click on the new field, and select **Field Calculator**. Input a formula to calculate the volume change,
and think about what units you want the resulting geodetic balances to be in (hint: they are currently in cubic meters).
Adjust the formula accordingly, and click **OK**.


.. card::
    :class-header: question
    :class-card: question

    :far:`circle-question` Question
    ^^^

    - What do you notice about the volume changes?
    - What could you do to calculate the area-averaged elevation change, instead of the volume change?
