gee tutorials
================

.. toctree::
   :glob:
   :hidden:
   :maxdepth: 2

   getting_started
   spectral
   vectors
   mapping
   band_maths
   classification/index
   advanced/index

In these tutorials, you'll get an introduction to using Google Earth Engine (GEE) for remote sensing analysis. 
Even if you have no prior experience with programming, you should be able to follow along with the examples.

If you're interested in learning a bit more, you can also check out Google's 
`Introduction to JavaScript for Earth Engine <https://developers.google.com/earth-engine/tutorials/tutorial_js_01>`__, 
which covers some more of the basics (at least enough to get you started).

For a more in-depth introduction to javascript, there are a number of free courses available online -- 
`Codecademy <https://www.codecademy.com/learn/introduction-to-javascript>`__'s javascript course is a good place to start. 

GEE is "a cloud-based platform for planetary-scale geospatial analysis" (Gorelick et al., 2017\ [1]_). With it, 
users have access to a number of tools, including entire satellite archives, machine-learning algorithms for classification, 
and computational power above what an average desktop user has access to.

In addition to being an introduction to GEE, these tutorials are also meant to serve as an introduction, or a refresher, 
on some of the fundamental concepts and techniques in remote sensing. The explanations will by no means be exhaustive, 
but they should serve as a starting point from which you can deepen your knowledge and understanding of remote sensing, 
and I will do my best to include links and references along the way.


getting an earth engine account
--------------------------------

If you do not already have an Earth Engine account set up, head on over to https://earthengine.google.com/ to sign up 
(click the 'Sign up' button in the upper right-hand corner of the page). If you already have a Google account, you can use 
that to sign up; otherwise, you can also set it up using a different e-mail address.


script repository
------------------

For each of the different tutorials, I've created a script that will show the different steps. You are welcome to use these, 
or create your own scripts using the sample code provided as you read through the tutorial.

You can access the repository (collection) of scripts `here <https://google.com>`__. *To be completed...*


data catalog
-------------

The `GEE data catalog <https://developers.google.com/earth-engine/datasets>`__ is vast and ever-growing. 
If you have a particular application in mind, be sure to have a look through the catalog - you might find a 
number of datasets that will help you. 

For the most part, these tutorials will stick to so-called **optical** images. **Optical sensors** use light
in the **visible** and **infrared** portions of the electromagnetic spectrum (between about 400 nm -- 3000 nm,
or up to about 12000 nm for **thermal infrared** wavelengths).

Optical sensors differ based on the wavelengths acquired and the general operation, but for the most part the
images look similar to what we can see with our eyes, which helps with interpretation. The optical sensors that
we will make use of in these tutorials will primarily be `Landsat <https://developers.google.com/earth-engine/datasets/catalog/landsat>`__
or `Sentinel-2 <https://developers.google.com/earth-engine/datasets/catalog/sentinel-2>`__ images, though we may 
use some others depending on the application.


contents
---------

- :doc:`getting_started`

    - adding images
    - inspector
    - exporting data


- :doc:`spectral`

    - adding geometries (points)
    - plotting

        - extracting data from points
        - aggregating to plot spectral signatures
        - export to png, csv, etc.

    - use different images to show spectral resolution


- :doc:`vectors`

    - importing vector data (country outlines?)
    - clipping using vector geometry


- manual mapping

    - mention GEEDiT
    - mosaicking cloud-free images
    - digitizing tools


- band maths

    - normalized difference indices
    - thresholding
    - edting polygons?
    - functions?
    

- change detection

    - multi-temporal classification (https://twitter.com/spatialthoughts/status/1328052808361275393)
    - change vector analysis (simple 2-band version)


- classification

    - pixel-based classification
    - object-based classification
    - accuracy analysis


- zonal stats?


- "advanced" topics

    - animated gif
    - land surface temperature?


references
----------

.. [1] Gorelick, N., M. Hancher, M. Dixon, S. Ilyushchenko, D. Thau, and R. Moore (2017). Google Earth Engine: Planetary-scale geospatial analysis for everyone. *Rem. Sens. Env.* 202, 18-27. doi: `10.1016/j.rse.2017.06.031 <https://doi.org/10.1016/j.rse.2017.06.031>`__





