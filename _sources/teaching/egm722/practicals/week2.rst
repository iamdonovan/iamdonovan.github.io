mapping with cartopy
==================================

In this practical, we'll create a map using similar data to what you used in the first practical of EGM711. This time,
rather than using ArcGIS Pro, we'll use ``cartopy``, ``matplotlib``, and ``geopandas``, python packages used for making
maps, plotting data, and working with vector data, respectively.

The practical this week is provided as a Jupyter Notebook, where you can interactively work through the different steps
of plotting the data. There is a second file, **practical2_script.py**, which will create the same map over again. Once
you have worked through the Jupyter Notebook, you can modify the script to complete the second part of the exercise,
and experiment with the different parameters used to make the map.

Getting started
---------------

To get started with this week's practical, first head to the your GitHub repository (:samp:`https://github.com/<{your_username}>/egm722`).
You should notice that this repository has 5 branches – you can click on the **branch** button to see all of the branches
available for a particular repository:

.. image:: ../../../img/egm722/week2/github.png
    :width: 720
    :align: center
    :alt: the github repository

|br| You should be able to see that the available branches are ``main``, the default **branch** that we used in last
week's practical, and branches for weeks 2 through 5.

If you open up the folder where you've **cloned** your repository, you should only see the **Week1** folder - no
**Week2**, **Week3**, and so on:

.. image:: ../../../img/egm722/week2/week1_folder.png
    :width: 600
    :align: center
    :alt: the repository folder showing only Week 1 materials

|br| We want to be able to work with each of the weeks at the same time, without having to switch branches each time.
To do this, we'll need to add each week's folder to the main branch.

Each week, we'll see how we can **merge**, or integrate, that week's branch into the ``main`` branch. This week, we'll
use **GitHub Desktop** to do this. In the coming weeks, we'll also introduce other options such as the command-line
interface or
`Pull Requests <https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests>`_.

For now, open up **GitHub Desktop**. You should see something like this:

.. image:: ../../../img/egm722/week2/desktop1.png
    :width: 600
    :align: center
    :alt: the github desktop window

|br| Click the button that shows the current branch (**main**) – you should see the following:

.. _desktop branches:

.. image:: ../../../img/egm722/week2/desktop_branches.png
    :width: 600
    :align: center
    :alt: the github desktop window

|br| In addition to your **local** ``main`` branch, you should also see **upstream** versions of each of the branches
(``main``, ``week2``--``week5``), as well as **origin** versions.

These are different things, and it's important to keep track of the differences:

- The **local** branches are the versions that are stored on *your* computer, *local*\ ly. 
- The **origin** branches are the versions stored on *your* GitHub repository
- The **upstream** branches are the versions that are stored in the repository that you forked from (https://github.com/iamdonovan/egm722)

Right now, you should only have the ``main`` branch on your machine. To work with (**checkout**) the ``week2`` branch,
we need to download it. Select the **origin** ``week2`` (``origin/week2``) branch, and **GitHub Desktop** will download
the files on the ``week2`` branch to your computer, and switch (**checkout**) the ``week2`` branch.

You should see that the "Current branch" has changed:

.. image:: ../../../img/egm722/week2/desktop_week2.png
    :width: 600
    :align: center
    :alt: the github desktop window

|br| And, you can see that the contents of your repository folder have changed:

.. image:: ../../../img/egm722/week2/week2_folder.png
    :width: 600
    :align: center
    :alt: the repository folder showing only Week 2 materials

|br| Remember - **the files are not gone**. When you switch from one branch to another, **git** changes the files in
the folder to reflect the state of the branch you're working on. Because there is no **Week1** folder on the ``week2``
branch, it's been temporarily removed. You can verify this by switching branches in **GitHub Desktop** and seeing how
the folder contents change.

.. warning::

    **Make sure that you're on the** ``main`` **branch before continuing**.

    As good practice, you should also click the "**Fetch origin**" button before continuing. 

    There shouldn't be many changes on the remote repository that aren't on your local computer, so this won't make
    much of a difference right now. If you're working collaboratively with others, though, it's good to make sure that
    you're not missing important changes before merging different branches.

To **merge** the two branches, click on the **Branch** menu, then select **Merge into current branch...**. In the menu
that opens, select the **local** ``week2`` branch:

.. image:: ../../../img/egm722/week2/merge_week2.png
    :width: 600
    :align: center
    :alt: merging the week2 branch into main using github desktop

|br| You should see that a green checkmark appears, indicating that there aren't any **conflicts** (files that have
been changed on both branches). The message:

    This will merge **2 commits** from **week2** into **main**

Tells us the number of commits that will be merged into ``main``. Note that you may see a different number of commits
here - as long as you have no conflicts, this isn't a problem.

Select **Create a merge commit** - this will create a new commit that merges the two branches together. For now, don't
worry about the other options for merging branches together.

Once you've created the merge commit, you should see that **Fetch origin** has changed to **Push origin** - this will
**push** (upload) the changes you've made locally to your **GitHub** repository:

.. image:: ../../../img/egm722/week2/desktop_push.png
    :width: 600
    :align: center
    :alt: pushing changes from the github desktop window

|br| Once the changes have been pushed, go back to your **GitHub** repository (:samp:`https://github.com/<{your_username}>/egm722`).
You should now see that your ``main`` branch has both the **Week1** and **Week2** folders:

.. image:: ../../../img/egm722/week2/github_merged.png
    :width: 720
    :align: center
    :alt: the github repository showing the merged files

|br| You can also confirm the changes in your **local** folder:

.. image:: ../../../img/egm722/week2/merged.png
    :width: 600
    :align: center
    :alt: the repository folder showing the merged materials

|br| At this point, you should be ready to open jupyter and work your way through the Week 2 Notebook, following the
same initial steps as last week.

Running the script
-------------------

To edit the script (**practical2_script.py**), open it in your IDE. If your IDE has a built-in terminal/python
interpreter, you can also run the script directly from the IDE:

.. image:: ../../../img/egm722/week2/pycharm.png
    :width: 720
    :align: center
    :alt: the script open in the pycharm IDE

|br| Otherwise, you can use the **command prompt**; the procedure will be effectively the same.

Launch the command prompt from **Anaconda Navigator**, taking care to ensure that your ``egm722`` environment is
selected (rather than the ``base`` environment). When it launches, you should see the following window:

.. image:: ../../../img/egm722/week2/prompt3.png
    :width: 600
    :align: center
    :alt: the conda prompt

|br|

.. note::

    If, instead of ``(egm722)``, you see ``(base)`` next to the command prompt, you will need to *activate* the correct
    environment by typing:

    .. code-block:: sh
    
        conda activate egm722 

    and pressing **ENTER**.

Navigate to the week 2 folder using the ``cd`` command. You should see the jupyter-notebook file, as well as the script:

.. image:: ../../../img/egm722/week2/week2_dir.png
    :width: 600
    :align: center
    :alt: the contents of the week 2 directory in the command prompt

|br| Remember that we can use python in two ways, either interactive or script mode. We also have a choice of two
different interpreters - either ``python`` (the standard python interpreter) or ``ipython`` (an enhanced interactive
interpreter).

I recommend using IPython instead of the standard interpreter when using interactive mode – the interpreter highlights
syntax, it keeps track of your sessions and enables you to easily look back over your command history, enables you to
use some shell commands from within the interpreter, and also enables tab completion for commands, variable names,
and filenames.

You can run any script from start to finish using either interpreter by typing ``python script.py`` (or
``ipython script.py``, although the benefits of using IPython come from running python in interactive mode rather than
script mode).

.. image:: ../../../img/egm722/week2/script_run.png
    :width: 600
    :align: center
    :alt: the result of running the script from the command prompt

|br| If you want to be able to troubleshoot the script, or run additional commands after the script has finished running,
you can also start the interpreter in interactive mode by typing ``ipython -i script.py``:

.. image:: ../../../img/egm722/week2/ipython_script.png
    :width: 600
    :align: center
    :alt: the result of running the script from the command prompt using ipython -i

|br| To show the plot, use ``plt.show()``:

.. image:: ../../../img/egm722/week2/plot.png
    :width: 600
    :align: center
    :alt: the plot window open from ipython

|br| You can also turn on interactive plotting using ``plt.ion()``, which will update the plot each time you run a
plotting command – similar to how it worked in the Jupyter Notebook.

Once you have finished the exercise, you can try adding other features to your map, work on re-creating some of the maps
that you created in EGM711, or try some of the examples shown on the
`cartopy website <https://scitools.org.uk/cartopy/docs/v0.13/matplotlib/intro.html>`_.
Can you work out how to include a basemap to your image, based on some of the examples provided?

.. note::
    
    Below this point is the **non-interactive** text of the notebook. To actually run the notebook, you'll need to
    follow the instructions above to open the notebook and run it on your own computer!

....

Ryan Gosling
------------------

In the first practical for EGM711, you learned how to use ArcGIS Pro to
make maps, given shapefiles of different features of interest in
Northern Ireland. In this practical, you will repeat the exercise, this
time using ``cartopy``, ``geopandas``, and ``matplotlib``, three python
packages used for making maps, working with vector data, and making
plots, respectively.

Objectives
.............

-  become familiar with geopandas, cartopy, and matplotlib, including
   reading the provided documentation
-  use list comprehensions to simplify some for loops

1. Getting started
.....................

First, run the cell below. It will load the python modules we’ll be
using in the practical, as well as define a few helper functions that
we’ll use later on. For now, don’t worry too much about what each
individual line does - we’ll go over these in a bit more depth as we go.
Remember also that if you get stuck, you can get help in a few ways:

1. the built-in help (i.e., ``help(plt.text)``)
2. using ipython’s (the python interpreter used by jupyter-notebooks)
   help shortcut (i.e., ``plt.text?``)
3. finding the online documentation for the module (usually achieved via
   option 4)
4. searching google (or your search engine of choice)
5. consulting your favorite medicine man/shaman/spiritual guide
6. asking the instructor, who will in all likelihood resort to one of
   the other options (usually 5 or 4).

.. code:: ipython3

    # this lets us use the figures interactively
    %matplotlib inline

    import os
    import geopandas as gpd
    import matplotlib.pyplot as plt
    from cartopy.feature import ShapelyFeature
    import cartopy.crs as ccrs
    import matplotlib.patches as mpatches
    import matplotlib.lines as mlines

    plt.ion() # make the plotting interactive

    # generate matplotlib handles to create a legend of the features we put in our map.
    def generate_handles(labels, colors, edge='k', alpha=1):
        lc = len(colors)  # get the length of the color list
        handles = []
        for i in range(len(labels)):
            handles.append(mpatches.Rectangle((0, 0), 1, 1, facecolor=colors[i % lc], edgecolor=edge, alpha=alpha))
        return handles

    # create a scale bar of length 20 km in the upper right corner of the map
    # adapted this question: https://stackoverflow.com/q/32333870
    # answered by SO user Siyh: https://stackoverflow.com/a/35705477
    def scale_bar(ax, location=(0.92, 0.95)):
        x0, x1, y0, y1 = ax.get_extent()
        sbx = x0 + (x1 - x0) * location[0]
        sby = y0 + (y1 - y0) * location[1]

        ax.plot([sbx, sbx - 20000], [sby, sby], color='k', linewidth=9, transform=ax.projection)
        ax.plot([sbx, sbx - 10000], [sby, sby], color='k', linewidth=6, transform=ax.projection)
        ax.plot([sbx-10000, sbx - 20000], [sby, sby], color='w', linewidth=6, transform=ax.projection)

        ax.text(sbx, sby-4500, '20 km', transform=ax.projection, fontsize=8)
        ax.text(sbx-12500, sby-4500, '10 km', transform=ax.projection, fontsize=8)
        ax.text(sbx-24500, sby-4500, '0 km', transform=ax.projection, fontsize=8)

    # load the outline of Northern Ireland for a backdrop
    outline = gpd.read_file(os.path.abspath('data_files/NI_outline.shp'))


2. Loading the data
......................

Great. Now that we’ve imported most of the modules we’ll be needing, and
defined a few helper functions, we can actually load our data. To load
the shapefile data, we will use `GeoPandas <http://geopandas.org/>`__,
an open-source package designed to make working with geospatial data in
python easier.

GeoPandas is built off of Pandas, a powerful data analysis tool. We will
be working with both of these packages more in the weeks to come.

To open a shapefile, we use the ``gpd.read_file()``
(`documentation <https://geopandas.org/en/stable/docs/reference/api/geopandas.read_file.html>`__)
method:

.. code:: ipython3

    towns = gpd.read_file(os.path.abspath('data_files/Towns.shp'))
    water = gpd.read_file(os.path.abspath('data_files/Water.shp'))
    rivers = gpd.read_file(os.path.abspath('data_files/Rivers.shp'))
    counties = gpd.read_file(os.path.abspath('data_files/Counties.shp'))

GeoPandas loads the data associated with a shapefile into a
GeoDataFrame, a tabular data structure that always has a column
describing a feature’s geometry. Each line in the table corresponds to a
feature in the shapefile, just like the attribute table you are familiar
with from ArcGIS/QGIS.

To see a subset of a GeoDataFrame, we can use the ``head()``
(`documentation <https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.head.html>`__)
method:

.. code:: ipython3

    water.head(10)

To select rows in the dataframe using an index, we can use ``.loc``
(`documentation <https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.loc.html>`__):

.. code:: ipython3

    water.loc[0] # should show the row for Lough Neagh

Note that ``.loc`` is not a method, since we use square brackets:``[``
and ``]``, instead of round brackets/parentheses. Instead, it’s a way to
index or slice a GeoDataFrame.

This means that we can also use ``.loc`` with conditional statements.
For example, if we wanted to select all bodies of water that are smaller
than 1 square kilometer, we could use something like this:

.. code:: ipython3

    water.loc[water['Area_km2'] < 1]

Note that with only a single value, ``.loc`` returns all columns of the
GeoDataFrame where the rows match the given index/conditional statement.

To select a specific column or group of columns, we can use a comma to
separate the different indexers. For example, if we want to select only
the name of the lakes that are smaller than 1 square kilometer, we can
use the following:

.. code:: ipython3

    water.loc[water['Area_km2'] < 1, 'namespace']

Each “column” of the GeoDataFrame is an object of type Series
(`documentation <https://pandas.pydata.org/docs/reference/api/pandas.Series.html>`__).

If a Series is filled with numeric data, we can use different methods
such as ``.sum()``
(`documentation <https://pandas.pydata.org/docs/reference/api/pandas.Series.sum.html>`__)
or ``.mean()``
(`documentation <https://pandas.pydata.org/docs/reference/api/pandas.Series.mean.html>`__),
to get the sum and mean of the values in the Series, respectively.

So, the total area (in square kilometers) of all of the lakes in the
dataset would be given by the following statement:

.. code:: ipython3

    water['Area_km2'].sum()

We’ll work with GeoDataFrames more in next week’s practical, but for now
see if you can put these different pieces together and figure out the
total area of lakes in the ``Water`` dataset that are smaller than 10
square kilometers. I’ll provide two hints to get you started:

1. GeoDataFrames can be subset using a conditional and a column in the
   GeoDataFrame, like we saw above.
2. With only a single value, ``.loc`` returns all columns of the
   GeoDataFrame where the rows match the given index/conditional
   statement. To select a specific column or group of columns, we can
   use a comma to separate the different indexers.
3. The numerical columns of a GeoDataFrame (also called Series or
   GeoSeries) have built-in operators such as **max**, **min**,
   **mean**, and so on.

That should be enough to get you started - if you get stuck, be sure to
ask for help.

.. code:: ipython3

    # write a statement (or series of statments) to calculate the total area of lakes < 10 km2 in the water dataset.

3. Creating maps with matplotlib and cartopy
...............................................

Now that we’re more familiar with the dataset, we can start building our
map. For this portion of the practical, we’ll be mostly using
`matplotlib <https://matplotlib.org/>`__, a python package designed for
making plots and graphs, and
`cartopy <https://scitools.org.uk/cartopy/docs/latest/>`__, a package
designed for making maps and representing geopatial data.

.. code:: ipython3

    myFig = plt.figure(figsize=(10, 10))  # create a figure of size 10x10 (representing the page size in inches)

    myCRS = ccrs.UTM(XX)  # create a Universal Transverse Mercator reference system to transform our data.
    # be sure to fill in XX above with the correct number for the UTM Zone that Northern Ireland is part of.

    ax = plt.axes(projection=myCRS)  # finally, create an axes object in the figure, using a UTM projection,
    # where we can actually plot our data.

Adding data to the map
^^^^^^^^^^^^^^^^^^^^^^

Now that we’ve created a figure and axes, we can start adding data to
the map. To start, we’ll add the municipal borders.

In order to add these to the map, we first have to create features that
we can add to the axes using the ``ShapelyFeature`` class from
``cartopy.feature``. The initialization method for this class takes a
minimum of two arguments, an **iterable** containing the geometries that
we’re using, and a CRS representation.

To add the County borders, then, we would use ``counties['geometry']``,
the GeoSeries of the feature geometries in our Municipalities shapefile,
and ``myCRS``, the CRS object representing the UTM Zone for Northern
Ireland:

.. code:: ipython3

    # first, we just add the outline of Northern Ireland using cartopy's ShapelyFeature
    outline_feature = ShapelyFeature(outline['geometry'], myCRS, edgecolor='k', facecolor='w')
    xmin, ymin, xmax, ymax = outline.total_bounds
    ax.add_feature(outline_feature) # add the features we've created to the map.

The other arguments that we pass to ``ShapelyFeature`` tell
``matplotlib`` how to draw the features - in this case, with an edge
color of black and a face color of gray. Once we’ve created the
features, we add them to the axes using the ``add_feature`` method.

We’ll also want to zoom the map into our area of interest using the
boundary of the shapefile features (using ``ax.set_extent``). In the
example below, we’re setting the extent with a 5 km buffer around each
edge:

.. code:: ipython3

    # using the boundary of the shapefile features, zoom the map to our area of interest
    ax.set_extent([xmin-5000, xmax+5000, ymin-5000, ymax+5000], crs=myCRS) # because total_bounds
    # gives output as xmin, ymin, xmax, ymax,
    # but set_extent takes xmin, xmax, ymin, ymax, we re-order the coordinates here.

    myFig ## re-draw the figure

This is fine, but a bit boring. For one thing, we might want to set
different colors for the different municipalities, rather than having
them all be the same color. To do this, we’ll first have to count the
number of **unique** municipalities in our dataset, then select colors
to represent each of them.

Question: Why might we do this, rather than just use the number of
features in the dataset?

Run the cell below to count the number of unique municipalities in the
dataset, using the ``unique`` method on the **CountyName** GeoSeries.

Note that in addition to the standard indexing (i.e.,
``counties['CountyName']``), we are accessing **CountyName** directly as
an attribute of ``counties`` (i.e., ``counties.CountyName``).

Provided that the column name follows particular rules (`more on this
here <http://pandas.pydata.org/pandas-docs/stable/indexing.html#attribute-access>`__),
there is no difference between these two methods - they give the same
results.

.. code:: ipython3

    # get the number of unique municipalities we have in the dataset
    num_counties = len(counties.CountyName.unique())
    print('Number of unique features: {}'.format(num_counties)) # note how we're using {} and format here!

Now that you’ve found the number of colors you need to choose, you can
use the image below to make a list of the colors. There are other ways
to select colors using matplotlib, including using RGB values, but
that’s for another day. If you’re interested in learning more, you can
check out the documentation
`here <https://matplotlib.org/stable/api/colors_api.html>`__.

|title|
`source <https://matplotlib.org/stable/gallery/color/named_colors.html>`__

.. |title| image:: ../../../img/egm722/week2/named_colors.png
    :alt: the named colors in matplotlib

.. code:: ipython3

    # pick colors for the individual county boundaries - make sure to add enough for each of the counties
    # to add a color, enclose the name above (e.g., violet) with single (or double) quotes: 'violet'
    # remember that each colors should be separated by a comma
    county_colors = []
    
    # get a list of unique names for the county boundaries
    county_names = list(counties.CountyName.unique())
    county_names.sort() # sort the counties alphabetically by name
    
    # next, add the municipal outlines to the map using the colors that we've picked.
    # here, we're iterating over the unique values in the 'CountyName' field.
    # we're also setting the edge color to be black, with a line width of 0.5 pt. 
    # Feel free to experiment with different colors and line widths.
    for ii, name in enumerate(county_names):
        feat = ShapelyFeature(counties.loc[counties['CountyName'] == name, 'geometry'], # first argument is the geometry
                              myCRS, # second argument is the CRS
                              edgecolor='k', # outline the feature in black
                              facecolor=county_colors[ii], # set the face color to the corresponding color from the list
                              linewidth=1, # set the outline width to be 1 pt
                              alpha=0.25) # set the alpha (transparency) to be 0.25 (out of 1)
        ax.add_feature(feat) # once we have created the feature, we have to add it to the map using ax.add_feature()

    myFig # to show the updated figure

Now that we’ve done this for the municipal boundaries, we can also do
this for the water datasets. Because we want the water bodies to be the
same symbology, we add them with a single use of **ShapelyFeature**:

.. code:: ipython3

    # here, we're setting the edge color to be the same as the face color. Feel free to change this around,
    # and experiment with different line widths.
    water_feat = ShapelyFeature(water['geometry'], # first argument is the geometry
                                myCRS, # second argument is the CRS
                                edgecolor='mediumblue', # set the edgecolor to be mediumblue
                                facecolor='mediumblue', # set the facecolor to be mediumblue
                                linewidth=1) # set the outline width to be 1 pt
    ax.add_feature(water_feat) # add the collection of features to the map

    myFig # to show the updated figure

We do the same thing with the rivers. However, because these are
**Line** objects, not **Polygon**\ s, we don’t set the ``facecolor``
property:

.. code:: ipython3

    river_feat = ShapelyFeature(rivers['geometry'], # first argument is the geometry
                                myCRS, # second argument is the CRS
                                edgecolor='royalblue', # set the edgecolor to be royalblue
                                linewidth=0.2) # set the linewidth to be 0.2 pt
    ax.add_feature(river_feat) # add the collection of features to the map

    myFig # to show the updated figure

For **Point** data, such as the town locations, we can use ``ax.plot()``
directly.

The code below will add a gray (``color='0.5'``) square (``'s'``) marker
of size 6 (``ms=6``) at each x, y location:

.. code:: ipython3

    # ShapelyFeature creates a polygon, so for point data we can just use ax.plot()
    town_handle = ax.plot(towns.geometry.x, towns.geometry.y, 's', color='0.5', ms=6, transform=myCRS)
    
    myFig # to show the updated figure

Adding labels and legends
^^^^^^^^^^^^^^^^^^^^^^^^^

Now that we have different colors for each of the county boundaries and
we’ve displayed lakes, rivers, and towns, it might be good to have a
legend to keep everything straight.

To do this, we get handles for each of the county boundaries, using the
colors we defined earlier. Here, we’re using our helper function
``generate_handles``, which returns a list of ``matplotlib`` handles
(i.e., the symbol that ``matplotlib`` uses to display the objects in the
figure), given a list of labels and colors.

We then do the same for the water bodies and rivers:

.. code:: ipython3

    # generate a list of handles for the county datasets
    # first, we add the list of names, then the list of colors, and finally we set the transparency
    # (since we set it in the map)
    county_handles = generate_handles(counties.CountyName.unique(), county_colors, alpha=0.25)

    # note: if you change the color you use to display lakes, you'll want to change it here, too
    water_handle = generate_handles(['Lakes'], ['mediumblue'])

    # note: if you change the color you use to display rivers, you'll want to change it here, too
    river_handle = [mlines.Line2D([], [], color='royalblue')]

Note that the names in our county dataset are all uppercase - that’s not
necessarily how we want to display them on the map. To change this, we
can use a string method called **title()**, which will capitalize the
first letter of each word in a string. We also have to do this for each
of the items in our list of names. We *could* write this as a **for**
loop, like this:

.. code:: python

   nice_names = []  # initalize an empty list
   for name in county_names:
       nice_names.append(name.title())

But, python offers another, cleaner option, called a `list
comprehension <https://docs.python.org/3/tutorial/datastructures.html#list-comprehensions>`__.
A list comprehension allows us to generate a new list from an existing
iterable. To write the same **for** loop above as a list comprehension
takes one line:

.. code:: ipython3

    # update county_names to take it out of uppercase text
    nice_names = [name.title() for name in county_names]

That’s it. This creates a new list by iterating over each of the items
in county_names, applying a method, **str.title()**, to each item. We’ll
work more with list comprehensions throughout the module, as they
provide a way to simplify some pretty complicated loops.

We can pass each of our lists of handles and labels to ``plt.legend``,
to generate a legend for the municipal boundaries data. Feel free to
experiment with the placement (by changing **loc** and/or
**bbox_to_anchor**), or the font size, the title font size, and so on.

.. code:: ipython3

    # ax.legend() takes a list of handles and a list of labels corresponding to the objects
    # you want to add to the legend
    handles = county_handles + water_handle + river_handle + town_handle # use '+' to concatenate (combine) lists
    labels = nice_names + ['Lakes', 'Rivers', 'Towns']

    leg = ax.legend(handles, labels, title='Legend', title_fontsize=12,
                     fontsize=10, loc='upper left', frameon=True, framealpha=1)

    myFig # to show the updated figure

Now that we have a legend, let’s go ahead and add grid lines to our
plot. I’ve chosen some default gridlines, but you can feel free to
change this.

What happens if you delete the first and/or last value from xlocs and
ylocs? Try it and see!

Can you change the labels to show only on the bottom and left side of
the map? To see, try looking at this
`example <https://scitools.org.uk/cartopy/docs/latest/gallery/gridlines_and_labels/gridliner.html>`__,
or at the
`documentation <https://scitools.org.uk/cartopy/docs/latest/reference/generated/cartopy.mpl.gridliner.Gridliner.html#cartopy.mpl.gridliner.Gridliner>`__.

.. code:: ipython3

    gridlines = ax.gridlines(draw_labels=True, # draw  labels for the grid lines
                             xlocs=[-8, -7.5, -7, -6.5, -6, -5.5], # add longitude lines at 0.5 deg intervals
                             ylocs=[54, 54.5, 55, 55.5]) # add latitude lines at 0.5 deg intervals
    gridlines.left_labels = False # turn off the left-side labels
    gridlines.bottom_labels = False # turn off the bottom labels

    myFig # to show the updated figure

Excellent. Now, let’s add text labels for each of our individual towns.
For each of the points representing our towns/cities, we can place a
text label. Look over the cell below, and make sure you understand what
each line is doing. If you’re not sure you understand, you can post your
questions on Blackboard.

.. code:: ipython3

    for ind, row in towns.iterrows(): # towns.iterrows() returns the index and row
        x, y = row.geometry.x, row.geometry.y # get the x,y location for each town
        ax.text(x, y, row['TOWN_NAME'].title(), fontsize=7, transform=myCRS) # use plt.text to place a label at x,y

    myFig # to show the updated figure

Last but not least, let’s add a scale bar to the plot. The scale_bar
function we’ve defined above will produce a scale bar with divisions at
10 and 20 km, with a location in the upper right corner as default. Try
to experiment with this a bit - can you design a scale bar with
divisions at 1, 5, and 10 km? It’s not as straightforward as it is in
ArcGIS, but it might provide an interesting challenge if you’re
interested in developing your programming skills a bit.

.. code:: ipython3

    scale_bar(ax)

    myFig # to show the updated figure

Finally, we’ll save our figure. The command written below will save the
figure to the current folder, in a file called ``map.png``, with no
border around the outside of the map, and with a resolution of 300 dots
per inch. As always, feel free to change these parameters.

.. code:: ipython3

    myFig.savefig('map.png', bbox_inches='tight', dpi=300)

Next steps
.............

In this directory, you should also have a python script,
**practical2_script.py**, which will create the same map that we’ve made
here (though perhaps with different colors).

Note that the **towns** dataset has an attribute, **STATUS**, that
describes whether the feature represents a **Town** (e.g., Coleraine),
or a **City** (e.g., Belfast). As a further exercise, see if you can
modify the script to plot all of the **Towns** with one marker (e.g.,
the gray square used above), and plot all of the **Cities** plot with a
different marker, then add these to the legend. For more information on
the available markers and colors for matplotlib, see the
`documentation <https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.plot.html>`__.
