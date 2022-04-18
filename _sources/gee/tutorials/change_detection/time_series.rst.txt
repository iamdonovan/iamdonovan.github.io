time series analysis
=====================


plotting time series
---------------------

The final portion of this practical will cover how we can get time series of data from images and visually inspect the results. 
To get started, uncomment this section (remove the ``/*`` from line 371 and the ``*/`` from line 431). The
first part of this section declares a variable, ``ndvi_patches``, that is made up of individual polygons imported at the top of the
script:

.. code-block:: javascript

    var ndvi_patches = ee.FeatureCollection([fastRegrowth, slowRegrowth, 
      forest, oldClearCut, newClearCut]);

The next sections of code here deal with loading Landsat images and filtering based space and cloud cover, similar to what we
have done in previous steps. After this section, these lines of code:

.. code-block:: javascript

    // combine tm, etm+, oli, and mss images, add an NDVI band, and sort by date.
    var allNDVI = mss.map(mssNDVI).merge(tm.merge(oli).map(getNDVI))
      .select('NDVI').sort('system:time_start');

merge the MSS, TM, ETM+, and OLI image collections, calculate the NDVI for each image, and sort by acquisition date. The next lines:

.. code-block:: javascript

    // plot a chart of the mean ndvi values, calculated using different polygons
    // representing different landcover areas
    var ndviChart = ui.Chart.image
      .seriesByRegion({
        imageCollection: allNDVI,
        regions: ndvi_patches, // average using the features in each ndvi patch
        reducer: ee.Reducer.mean(),
        seriesProperty: 'label', // use the label values to plot individual series
        scale: 100,
        xProperty: 'system:time_start'})
      .setOptions({
        title: 'Mean NDVI',
        hAxis: {title: 'date', titleTextStyle: {italic: false, bold: true}},
        vAxis: {title: 'ndvi value', titleTextStyle: {italic: false, bold: true}},
        curveType: 'function'})
      .setSeriesNames(['ndvi']);
    print(ndviChart);

will plot the average values for each of the individual polygons in ``ndvi_patches``. You can see what this looks like below. Note
that some of the apparent lack of seasonality before about 2000 is mostly a result of the lower temporal resolution – Landsat
acquisitions were often limited during this time, and so some years will only have a few available images.

.. image:: ../../../img/egm702/week4/ndvi_timeseries.png
    :width: 600
    :align: center
    :alt: a time series of ndvi values for different polygons

If you open the chart (click on the icon in the upper right-hand corner), you can export the data as a CSV file for further analysis.

You can also add (or remove) polygons from the plot. To add your own polygon, you can use the digitizing tools located in the
upper left-hand corner of the map panel:

.. image:: ../../../img/egm702/week4/digitizing_tools.png
    :width: 600
    :align: center
    :alt: the digitizing tools panel highlighted

Be sure to start the polygon as a new layer (click on **+ new layer** at the bottom of the **Geometry Imports** panel):

.. image:: ../../../img/egm702/week4/geometry_imports_panel.png
    :width: 600
    :align: center
    :alt: the geometry imports panel expanded

Next, start digitizing a polygon – try to make sure that the polygon represents one type of area. Remember that you can use the
Landsat images, as well as the background satellite images, to help you. From the **Geometry Imports** panel, click the gear icon
next to your new layer to change the properties:

.. image:: ../../../img/egm702/week4/configure_import1.png
    :width: 300
    :align: center
    :alt: the configure geometry import panel

Change the name to something other than ``geometry`` (or ``example``), then change it to **Import as** a ``Feature``, and click to add
property to the feature. Call it ``label``, and add a value for the label.

.. image:: ../../../img/egm702/week4/configure_import2.png
    :width: 300
    :align: center
    :alt: the configure geometry import panel

Click **OK**, then digitize your polygon (if you haven’t already). Note that each feature can only contain a single polygon – to add
multiple polygons, you’ll need to create multiple features. You can then update ``ndvi_patches`` and re-run the script to update
the chart:

.. image:: ../../../img/egm702/week4/updated_ndvi_timeseries.png
    :width: 600
    :align: center
    :alt: the ndvi time series with the new polygon layer added

Feel free to try different polygons, and examine the different time series plots – try using the CVA angle map to help you decide
areas to look further into.

This is the end of this Practical – next week, we’ll look into using Earth Engine to do some more advanced classification
techniques, and run an accuracy analysis on the results.

