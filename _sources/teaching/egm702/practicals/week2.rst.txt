week 2 - dem differencing
=========================

introduction
------------

**Be sure to download all the data from the Practical 1 area on Blackboard before starting, or from the** `google drive link <https://google.com>`__\ **, then extract the zip file. You should
have the following files/folders available:**
::

    ├─ 1979_shapes.*
    ├─ 1984_shapes.*
    ├─ ALPSMLC30_N046W123_DSM.tif
    ├─ MtStHelens_Aug1984_10m_Z.tif
    ├─ MtStHelens_Jul1979_10m_Z.tif
    ├─ LM02_L1TP_049028_19790719_20180419_01_T2.tif
    ├─ LT05_L1TP_046028_19840804_20161004_01_T1.tif

You should also still have the NAIP images we used in Week 1. In this practical, we’re going to work on analysing the provided digital elevation models (DEMs) – their accuracy, and the spatial autocorrelation between the two air photo DEMs (**MtStHelens_Aug1984_10m_Z.tif** and **MtStHelens_Jul1979_10m_Z.tif**). We will also do some different calculations, including estimating the volume/mass of the mountain that collapsed, estimating changes in lake volume, and estimating the average height of trees that were knocked over by the blast.

If you aren’t familiar with the 1980 eruptions of Mt St Helens, here are some links that show some of the details:

- 1980 Eruption of Mt St Helens [`ArcGIS Online <https://www.arcgis.com/apps/Cascade/index.html?appid=f5c8638734254e20bd1d4a6db68aec05>`__]
- World of Change: Devastation and Recovery at Mt St Helens [`NASA Earth Observatory <https://earthobservatory.nasa.gov/world-of-change/StHelens>`__]
- Footage of the 1980 Mt St Helens Eruption [`YouTube <https://www.youtube.com/watch?v=AYla6q3is6w>`__]

getting started
---------------

Open up ArcGIS Pro, and create a new project in your Week 2 folder. You may need to add a folder connection to your Week 2 folder – if so, do that now.

Import the provided data into the map, re-arranging the drawing order as follows:

- 1979_shapes
- 1984_shapes
- MtStHelens_Jul1979_10m_Z.tif
- MtStHelens_Aug1984_10m_Z.tif
- ALPSMLC30_N046W123_DSM.tif
- LM02_L1TP_049028_19790719_20180419_01_T2.tif
- LT05_L1TP_046028_19840804_20161004_01_T1.tif

Change the Map coordinate system from WGS84 geographic coordinates to WGS84 UTM Zone 10N. You are hopefully already familiar with Landsat data from previous modules (the **LM02** file is a Landsat 2 MSS scene, and the **LT05** file is a Landsat 5 TM scene), but if not you can have a look at the `USGS Landsat missions <https://www.usgs.gov/core-science-systems/nli/landsat/landsat-satellite-missions>`__ page. 

Change the display of both images to be a false-colour infrared composite. For the MSS scene, this means setting the **Red channel** to be **Band_3** (MSS Band 6), the **Green channel** to be **Band_2** (MSS Band 5), and the **Blue channel** to be **Band_1** (MSS Band 4). For the TM scene, this means setting Red, Green, Blue to be **Band_4**, **Band_3**, and **Band_2**, respectively.

Next, we’re going to add hillshades of our DEMs to the map. You may notice that it’s not easy to interpret the DEM when it’s displayed in the default way – for one thing, the upper part of the volcano is washed out, while some of the lower-lying areas are quite dark. By adding a hillshade, we can make it easier to see a large range of elevations. 

From the **Analysis** tab, click on **Tools**:

**toolbar image**

In the search bar that pops up, type “hillshade” and press **Enter**. Select the **Hillshade** tool from the **Spatial Analyst** toolbox:

**hillshade dialogue**

Select the 1979 DEM as the **Input raster**, and save the output as `MtStHelens_Jul1979_10m_HS.tif`. Leave the other
parameters as the default values, then click **Run** at the bottom of the panel. Next, change the symbology of
`MtStHelens_Jul1979_10M_Z.tif` to use a different colour scheme. The example below is using **Elevation #4**. Finally,
change the **Transparency** of the DEM layer to be about 60% transparent:

**transparency**

Finally, right-click on the **Map** layer in the Contents panel, create a **New Group Layer** and call it `1979 Elevation`, then add the
DEM and the Hillshade to this layer (click + drag on the Contents panel). Your map should now look something like this:

**shaded relief image**

Repeat these steps for the remaining two DEMs – you can call the `ALPSMLC30...` layer 2008 Elevation. You should now see all 3
of the DEMs as shaded relief. You may also notice that the colour scheme for each of the DEMs is slightly different. To make sure
that the same colours correspond to the same elevations in each map, you can import the settings from one DEM to the other
ones under the **Symbology** tab. Press the button in the upper right corner of the tab, then select **Import from layer**:

**symbology**

Under Input layer, select the DEM you want to apply the colour scheme to, then select the DEM whose colour scheme you want
to apply (in this case, the 1979 DEM). You can do this for both the 1984 and 2015 DEMs – you should now see that the DEMs all
have the same colour scheme:

**common color scheme**

Take a few moments to examine the differences between them – you can even use the Swipe tool under the Appearance tab to
swipe back and forth between different DEMs – make sure that the DEM you want to swipe away is highlighted in the Contents
panel. You should be able to clearly see the enormous differences that took place between the 1979 acquisition and the 1984
acquisition. In the remainder of the practical, we will work on quantifying these differences. If you haven’t already, this is a good
place to save your map.

dem differencing
----------------



