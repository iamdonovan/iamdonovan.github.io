searching for images with sentinelsat
=======================================


getting started
-----------------

The other thing you'll need to do before starting this week's practical is install a new python package,
**sentinelsat**, into our **conda** environment.

First, open up **Anaconda Navigator**. Make sure to switch to your ``egm722`` environment, then click on the
**Environments** tab:

.. image:: ../../../img/egm722/week4/environments.png
    :width: 720
    :align: center
    :alt: the "environments" tab in Anaconda Navigator, opened on the egm722 environment

|br| Change the list from **Installed** to **Not installed**, then type ``sentinel`` into the **Search** bar in the
upper right-hand corner:

.. image:: ../../../img/egm722/week4/package_search.png
    :width: 720
    :align: center
    :alt: the "environments" tab in Anaconda Navigator, showing all packages that match 'sentinel'

.. note::

    If nothing shows up here, don't panic:

    .. image:: ../../../img/egm722/week4/blank_search.png
        :width: 600
        :align: center
        :alt: the "environments" tab in Anaconda Navigator, showing all packages that match 'sentinel'

    It just means we need to add the ``conda-forge`` channel to the list of **Channels**.

    To do this, first click the **Channels** button, then type ``conda-forge``:

    .. image:: ../../../img/egm722/week4/add_channel.png
        :width: 300
        :align: center
        :alt: adding a new channel called "conda-forge" to the list of channels

    Press **Enter**, and you should see the new channel added to the list:

    .. image:: ../../../img/egm722/week4/channels_added.png
        :width: 300
        :align: center
        :alt: the new channel added to the list of channels

    Click **Update channels**. Once the channel list finishes refreshing, you should see the ``sentinelsat`` package
    in the list of available packages.


Click the box next to ``sentinelsat`` to select it, then click **Apply** in the lower right-hand corner:

.. image:: ../../../img/egm722/week4/package_select.png
    :width: 720
    :align: center
    :alt: the "environments" tab in Anaconda Navigator, with the 'sentinelsat' package selected

|br| You should see the following window open (note that this may take some time):

.. image:: ../../../img/egm722/week4/package_install.png
    :width: 300
    :align: center
    :alt: the list of new packages to add to the environment

|br| Click **Apply**, and the packages will be downloaded/installed in the environment. While you wait for **Anaconda**
to finish working, you will be able to move on to the next steps.

Alternatively, go and grab a coffee or tea, and move on to the next steps.


the .netrc file
-----------------

In order to search for and download data using the sentinelsat API, we will need to authenticate (log in) using your
Copernicus Open Access Hub username/password.

The ``SentinelAPI`` (`documentation <https://sentinelsat.readthedocs.io/en/stable/api_reference.html#sentinelsat.sentinel.SentinelAPI>`__)
class takes your username and password as arguments:

.. code-block:: python

    connection = SentinelAPI(user, password)

However, typing your password in like this is not a good idea, security-wise.

.. danger::

    No, seriously. **NEVER**, **EVER** type your password in plaintext in a script or a jupyter notebook.

Instead, what we'll set up is something called a netrc or ``.netrc`` file\ [1]_, which ``SentinelAPI`` can read to
authenticate you with the Copernicus Open Access Hub.

A `netrc file <https://www.gnu.org/software/inetutils/manual/html_node/The-_002enetrc-file.html>`__ can be used by a
number of websites and programs for authentication, making it so that you don't type your password as plaintext in a
script or command prompt.

The ``.netrc`` file is a text file with a simple structure, where each line corresponds to a "machine" or website:

.. code-block:: text

    machine <website> login <username> password <password>

To create the file, open **notepad++** (or **notepad**, or your text editor of choice), and enter the following line:

.. code-block:: text

    machine apihub.copernicus.eu login <username> password <password>

remembering to replace :samp:`<username>` with your Copernicus Open Access Hub username, and :samp:`<password>` with
your Copernicus Open Access Hub password.

Save the file as ``.netrc`` to your **Home** directory (on Windows, this should be ``C:\Users\<your_username>``).
Be sure to select **All Files** for **Save as type**:

.. image:: ../../../img/egm722/week4/saveas_notepad.png
    :width: 600
    :align: center
    :alt: the "save as" window for notepad

|br| From **notepad++**, you should also uncheck **Append extension**:

.. image:: ../../../img/egm722/week4/saveas_notepadpp.png
    :width: 600
    :align: center
    :alt: the "save as" window for notepad++

|br| We're not quite done - there's one last thing we'll need to do before moving on.

changing permissions
.......................

.. note::

    On MacOS or linux-based systems, enter the following command in a terminal window:

    .. code-block::

        chmod 600 ~/.netrc

    This uses the ``chmod`` command to change the permissions on the file so that only the *owner* of the file has
    read/write access to the file (for more about ``chmod`` permissions, see this
    `wikipedia entry <https://en.wikipedia.org/wiki/Chmod>`__).


The last step we want to do in setting up the netrc file is to change the *permissions* so that other users can't
access the file. To change the permissions of the file in Windows, first open **Windows Explorer**.

From **Windows Explorer**, right-click on the file and select **Properties**:

.. image:: ../../../img/egm722/week4/properties.png
    :width: 300
    :align: center
    :alt: file properties for the new .netrc file

|br| Click on the **Security** tab:

.. image:: ../../../img/egm722/week4/security_orig.png
    :width: 300
    :align: center
    :alt: security properties for the new .netrc file

|br| then click **Advanced**:

.. image:: ../../../img/egm722/week4/advanced_orig.png
    :width: 600
    :align: center
    :alt: advanced security settings for the new .netrc file

|br| Click **Disable inheritance**, then click **Convert inherited permissions into explicit permissions on this object**
in the window that pops up:

.. image:: ../../../img/egm722/week4/block_inheritance.png
    :width: 400
    :align: center
    :alt: a dialogue asking what to do with the current inherited permissions for the .netrc file

|br| Now click **Apply**. Next, remove all of the rows from the table that aren't your user name (this should be
**SYSTEM** and **Administrators**):

.. image:: ../../../img/egm722/week4/advanced_end.png
    :width: 600
    :align: center
    :alt: advanced security settings for the new .netrc file, with only the user permissions set

|br| Click **Apply**, then highlight your username and click **Edit**. In the window that opens up, uncheck
**Full control**, but make sure that the other 4 available boxes are checked:

.. image:: ../../../img/egm722/week4/permissions_edited.png
    :width: 600
    :align: center
    :alt: the user permissions set so that the file owner can modify, read & execute, read, and write to the file.

|br| Click **OK**, then **OK** again to close the advanced security settings. You should see the permissions for the
file have changed:

.. image:: ../../../img/egm722/week4/security_final.png
    :width: 300
    :align: center
    :alt: file properties for the new .netrc file, updated so that only the file owner has access

|br| That's it - you should now be able to work through the notebook (assuming that you have correctly entered your
credentials in the ``.netrc`` file, that is).

At this point, you can launch Jupyter Notebooks from the command prompt, or from Anaconda Navigator, and begin to work
through the exercise.

.. note::

    Below this point is the **non-interactive** text of the notebook. To actually run the notebook, you'll need to
    follow the instructions above to open the notebook and run it on your own computer!


Gena Rowlands
---------------

Overview
..........

Up to now, you have gained some experience working with basic features
of python, used cartopy and matplotlib to create a map, explored using
shapely and geopandas to work with vector data, and explored using
rasterio and numpy to work with raster data.

In this example, we’ll see how we can use an application programming
interface (API) to query and download Sentinel data, using the
`SentinelSat <https://sentinelsat.readthedocs.io/en/stable/>`__ API. As
part of this, we’ll also introduce a few more geometric operations using
``shapely`` that you may find useful.

Objectives
............

In this example, you will:

-  Use ``shapely`` to get the *unary union* of a collection of shapes
-  Use ``shapely`` to find the minimum bounding rectangle of a geometry
-  Use the SentinelAPI to search for Sentinel-2 images
-  Calculate the fractional overlap between shapes
-  Use the SentinelAPI to download images

Data provided
...............

In this example, we will be using the ``Counties`` shapefile that we
used in Week 2.

1. Getting started
....................

To get started, run the following cell to import the packages that we’ll
use in the practical.

.. code:: ipython3

    import os
    import geopandas as gpd
    from sentinelsat import SentinelAPI, make_path_filter
    from IPython import display # lets us display images that we download
    import shapely

2. Prepare a search area
...........................

Before we get to using the API to search for images, we’ll see how we
can use existing data, like the ``Counties`` shapefile we used in Week
2, to help us search for images.

We won’t be able to use particularly complicated shapes, but we can use
a combination of GIS/geometric operations to get a simple outline of our
data, which can be used for the search.

First, we’ll load the data using ``geopandas``:

.. code:: ipython3

    counties = gpd.read_file('data_files/Counties.shp').to_crs(epsg=4326)

Next, we’ll use
`geopandas.Series.unary_union <https://geopandas.org/en/stable/docs/reference/api/geopandas.GeoSeries.unary_union.html>`__
to combine all of the County outlines into a single shape:

.. code:: ipython3

    # gets a single polygon (or multipolygon) composed of the individual polygons
    outline = counties['geometry'].unary_union

    outline # in jupyter notebook, this actually displays the polygon.

In the output of the cell above, we can see that the ``outline`` shape
is the combination of all of the individual county outlines.

We could use this as an input to our search, but we’ll look at one
additional operation that we can use to get a bounding box of the
geometry - the ``minimum_rotated_rectangle``:

.. code:: ipython3

    # gets the minimum rotated rectangle that covers the outline
    search_area = outline.minimum_rotated_rectangle

    search_area

You can see above that this gives a boundary box of the polygon, but
rather than being a simple rectangle made of the maximum/minimum
coordinates, it’s rotated to be as small as possible while still
covering the entire geometry.

This way, we minimize the area outside of the area of interest (Northern
Ireland) within our search area, while still making sure to cover the
entire area of interest.

Finally, if we look at the docstring for
`SentinelAPI.query() <https://sentinelsat.readthedocs.io/en/latest/api_reference.html#sentinelsat.sentinel.SentinelAPI.query>`__,
we see that the ``area`` argument needs to be a ``str``:

.. code:: ipython3

    help(SentinelAPI.query)

Specifically, it needs to be a `“Well-Known Text
(WKT)” <https://en.wikipedia.org/wiki/Well-known_text_representation_of_geometry>`__
representation of the geometry.

For a ``shapely`` geometry, the WKT representation of the geometry is
stored in the ``wkt`` attribute:

.. code:: ipython3

    # displays the search area wkt
    print(search_area.wkt)

That’s all we need to be able to search for images that intersect with a
given geometry. Once we have this, we can connect to the API and start
the query.

3. Search the archive for images
...................................

3.1 Connect to the api
~~~~~~~~~~~~~~~~~~~~~~

To connect to the API, we first create a
`SentinelAPI <https://sentinelsat.readthedocs.io/en/latest/api_reference.html#sentinelsat.sentinel.SentinelAPI>`__
object:

.. code:: python

   api = SentinelAPI(user, password)

From the API reference for ``sentinelsat``, we can see that we either
type in the username and password as a string, or we use ``None`` to use
the ``.netrc`` file that we created earlier:

.. code:: ipython3

    api = SentinelAPI(None, None) # remember - don't type your username and password into a jupyter notebook!

If there are no error messages or warnings, the connection was
successfully created, and we can move on to searching for images.

3.2 Search for images
~~~~~~~~~~~~~~~~~~~~~

As we saw earlier, the method we’ll use is ``api.query()``.

For this example, we’ll use the following arguments for the search:

-  ``area``: the search area to use
-  ``date``: the date range to use. We’ll look for all images from
   February 2023.
-  ``platformname``: we’re going to limit our search to Sentinel-2, but
   there are other options available
-  ``producttype``: we’ll search for the Sentinel-2 MSI Level 2A
   (surface reflectance) products
-  ``cloudcoverpercentage``: we want (mostly) cloud-free images, so
   we’ll search for images with < 30% cloud cover

To see what additional arguments are available, you can check the
`SentinelAPI <https://sentinelsat.readthedocs.io/en/latest/api_reference.html#sentinelsat.sentinel.SentinelAPI.query>`__
API reference, or the `Open Access
Hub <https://scihub.copernicus.eu/twiki/do/view/SciHubUserGuide/FullTextSearch?redirectedfrom=SciHubUserGuide.3FullTextSearch>`__
API reference for additional keywords to use.

.. code:: ipython3

    products = api.query(search_area.wkt, # use the WKT representation of our search area
                         date=('20230201', '20230228'), # all images from February 2023
                         platformname='Sentinel-2', # the platform name is Sentinel-2
                         producttype='S2MSI2A', # surface reflectance product (L2A)
                         cloudcoverpercentage=(0, 30)) # limit to 10% cloud cover

The output of ``api.query()`` is a ``dict()``, with the product name the
``key`` and the ``value`` being the metadata.

To see how many images were returned by the search, we can check the
length of the ``dict`` object, which tells us the number of ``item``\ s
(``key``/``value`` pairs) in the ``dict``:

.. code:: ipython3

    nresults = len(products)
    print('Found {} results'.format(nresults))

You should hopefully see that the search has returned 11 results.

To look at the first one returned, we can use the built-ins
`next() <https://docs.python.org/3/library/functions.html#next>`__
and
`iter() <https://docs.python.org/3/library/functions.html#iter>`__,
which returns the first item that was entered into the ``dict``:

.. code:: ipython3

    result = next(iter(products)) # get the "first" item from the dict
    products[result] # show the metadata for the first item

And, we can also download the browse image for this product, using
`SentinelAPI.download_quicklook() <https://sentinelsat.readthedocs.io/en/latest/api_reference.html#sentinelsat.sentinel.SentinelAPI.download_quicklook>`__:

.. code:: ipython3

    qlook = api.download_quicklook(result) # download the quicklook image for the first result
    display.Image(qlook['path']) # display the image

In this example, we might notice a small problem - while this image
technically does intersect our area of interest, it does so only barely.
Northern Ireland is the small bit of land in the lower left-hand corner
of this image - most of the image is of Scotland and the Irish Sea.

In the next section, we’ll see one way that we can make sure that we’re
only getting images that mostly intersect with our area of interest.

4. Filtering by overlap
.........................

To start, we use
`SentinelAPI.to_geodataframe() <https://sentinelsat.readthedocs.io/en/latest/api_reference.html#sentinelsat.sentinel.SentinelAPI.download_quicklook>`__
to convert the results into a ``GeoDataFrame``:

.. code:: ipython3

    product_geo = SentinelAPI.to_geodataframe(products) # convert the search results to a geodataframe
    product_geo.head() # show the first 5 rows of the geodataframe

Now, we can iterate over ``GeoDataFrame`` to calculate the intersection
of the image footprint with the outline of Northern Ireland:

.. code:: ipython3

    for ind, row in product_geo.iterrows():
        intersection = outline.intersection(row['geometry']) # find the intersection of the two polygons
        product_geo.loc[ind, 'overlap'] = intersection.area / outline.area # get the fractional overlap

    print(product_geo.overlap) # show the fractional overlap for each index

In this example, the third image,
``80558644-2e31-48b9-acd5-5d1475dfc1bf`` has 43% overlap with the
outline of Northern Ireland; none of the other images have more than
20%.

Rather than copying this down, we can use
``geopandas.GeoSeries.argmax()`` to find the integer location of the
largest value in the ``overlap`` column:

.. code:: ipython3

    max_index = product_geo.overlap.argmax() # get the integer location of the largest overlap value
    print(max_index) # should be 2

Then, we get the ``GeoDataFrame`` index that corresponds to that integer
location:

.. code:: ipython3

    best_overlap = product_geo.index[max_index] # get the actual index (image name) with the largest overlap
    print(product_geo.loc[best_overlap]) # show the metadata for the image with the largest overlap

With this, we can use ``api.download_quicklook()`` to download the
quicklook image for the result that has the largest overlap with the
outline of Northern Ireland:

.. code:: ipython3

    qlook = api.download_quicklook(best_overlap) # download the quicklook image for the first result
    display.Image(qlook['path']) # display the image

So that’s a little bit better - at least with this image, we can see
much more of Northern Ireland (and the ever-present clouds).

That’s all for right now - the next few cells provide examples for how
you can download the actual image data.

5. Downloading images
........................

Remember that these are very large files (each granule is ~1GB), so you
should only run these cells if you actually want to download the data!

download an individual image
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

We can use ``SentinelAPI.download()`` to download a single product:

.. code:: ipython3

    api.download(best_overlap) # downloads the first result

download an individual image, but only the image bands
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This example uses the ``nodefilter`` argument to only download the image
bands (files that match the format ``*_B*.jp2``):

.. code:: ipython3

    api.download(first_result, # downloads the first result
                 nodefilter=make_path_filter("*_B*.jp2")) # only download the image bands (optional)

download all images from a list of products
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

``SentinelAPI.download_all()`` will download all of the products in a
list.

Again, these are very large files, so you should only run the following
cell if you actually want to download all of the images returned by the
API!

.. code:: ipython3

    api.download_all(products,
                     n_concurrent_dl=5, # allow up to 5 concurrent downloads
                     nodefilter=make_path_filter("*_B*.jp2")) # only down the image bands (optional)


notes and references
-----------------------

.. [1] on Windows, some programs may look for a ``_netrc`` file in your **Home** directory, rather than ``.netrc``.