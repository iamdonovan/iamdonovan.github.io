image collections and vectors
==============================

plan:

    - adding imports (show steps)
    - filtering FC (to select a single boundary)
    - filtering IC (to get images that match different criteria)
    - functions, mapping (cloud mask)
    - mosaicking using median (mention others)
    - buffering geometries/features
    - clipping images to geometries
    - export to drive




adding dataset imports
------------------------

to import GEE datasets, add the following:

.. code-block:: 

    var borders = ee.FeatureCollection("FAO/GAUL/2015/level0");

Note that this gets underlined in yellow - mouse over, click "convert" -> added as import.

- import vector data (country outlines - iceland)
- select one vector (michigan)
- add vector layers to the map

- import MODIS image (?)

- clip image to feature

- add to map





