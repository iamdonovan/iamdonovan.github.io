pixel-based classification
==================================

Lorem ipsum, etc.


In this tutorial, ...

adding training points
--------------------------

To run a supervised classification, we need to provide **labeled training** data - that is, a number of points where
we have identified what **class** the points belongs to. 

The classification algorithm then takes these points, and the associated input data such as reflectance in different bands,
and determines the "rules" for how to classify points based on the input data.

When you open the script, you should see there are a number of **Geometry Imports**:

**script open**

Specifically, there are five **FeatureCollection** imports representing landcover classes (``water``, ``forest``, ``grassland``, ``builtup``,
and ``bare``), each with 40 points. To add more points to each of these, you can use the **Geometry Editing** tools:

**geometry imports**

Click on the layer that you want to add points to - for example, ``water``:

**water highlighted**

Then, click on the map to add the point:

**point added**

If you want to move or delete a point, click on the **Stop drawing** button (the hand), then select the point you
want to edit:

**point selected**

Then, either click and drag to move the **Point**, or click on **Delete** to delete the **Point**. 

.. note::

    For the purposes of this tutorial, 40 points for each class is sufficient to give you an idea for how the process works.
    To get a robust classification result and accuracy assessment, however, you will most likely need to add significantly more training
    points.


adding classes
---------------

You might also want to add additional landcover classes to the classification by adding a new **FeatureCollection** as follows.
First, mouse back over the **Geometry Imports**. At the bottom of the **Geometry Imports** menu, click on "**new layer**" 
to add a new layer, then click on the gear icon to open the configuration panel:

.. image:: img/spectral/configuration_panel.png
    :width: 600
    :align: center
    :alt: the configuration panel for the geometry imports

As a reminder, when adding geometry features from the map, you can choose to import them as a **Geometry**, a **Feature**,
or a **FeatureCollection**:

- **Geometry** means only vector data (no attributes/properties)
- **Feature** means you can have a geometry and attributes/properties, it will be treated as a single feature by GEE. So, if you have multiple points in a **Feature**, it will be imported as a **MultiPoint Feature**
- **FeatureCollection** means that each geometric object is treated as a **Feature** -- so, multiple points are treated as individual points. 

Make sure that you add the new class as a **FeatureCollection**, and give it an appropriate name. Next, click the **+property** button to add a new property:

.. image:: img/spectral/new_property.png
    :width: 400
    :align: center
    :alt: the configure geometry import panel with a new property

Call this property ``landcover`` (left box), and give it a value of ``5`` (right box), since landcover values 0-4 currently
correspond to the 5 classes that have already been imported.

Change the color to something more appropriate, then click **OK**. You should now see the import at the top of the script.

You can now add points to the new **FeatureCollection** by following the digitizing instructions from above.

Finally, you need to make sure to add your new class to the **FeatureCollection** of training points in the script at line 11:

.. code-block:: javascript

    var trainingPoints = water
      .merge(forest)
      .merge(grassland)
      .merge(builtup)
      .merge(bare);

To do this, delete the semicolon at the end of line 11, and add ``.merge(yourNewClass);`` on line 12 (remembering, of course, to replace
``yourNewClass`` with the actual name of the **FeatureCollection**).

splitting the training dataset
-------------------------------

Once we have training points, we can use ``ee.Image.sampleRegions()`` 
(`documentation <https://developers.google.com/earth-engine/apidocs/ee-image-sampleregions>`__) to get the **Image** values at those
points, which is what we'll use to train the **Classifier**:

.. code-block:: javascript

    var bands = ['SR_B1', 'SR_B2', 'SR_B3', 'SR_B4', 'SR_B5', 'SR_B6', 'SR_B7'];

    var training = img.select(bands).sampleRegions({
      collection: trainingPoints,
      properties: ['landcover'],
      scale: 30
    });

This will select each of the bands in ``bands``, then extract the values at each of the points in the ``trainingPoints``
**FeatureCollection**. To make sure that we include the ``landcover`` value for each point, we add this to the 
``properties`` parameter when we call ``ee.Image.sampleRegions()`` - otherwise, this information wouldn't be included
in the training dataset.

The next step in training a **Classifier** is to *split* the training dataset into two parts: one, the *training* split,
is what we'll use to actually train the **Classifier**. The second part, the *testing* split, is what we'll use to
check how good a job the **Classifier** has actually done. The goal here is to make sure that the

To split our dataset, we first use ``ee.FeatureCollection.randomColumn()``
(`documentation <https://developers.google.com/earth-engine/apidocs/ee-featurecollection-randomcolumn>`__). This will
add a column, ``'random'``, to the **FeatureCollection**, and fill the column with uniformly-distributed random
numbers that fall in the range [0, 1).

We then use ``ee.FeatureCollection.filter()`` to select the **Feature**\ s where the random value is less than 0.7,
which form our *training* data, and the **Feature**\ s where the random value is greater than or equal to 0.7,
which form our *testing* data:

.. code-block:: javascript

    var split = 0.7;
    var withRandom = training.randomColumn('random');
    var trainingPartition = withRandom.filter(ee.Filter.lt('random', split));
    var testingPartition = withRandom.filter(ee.Filter.gte('random', split));

training a classifier
----------------------

Once we've split the input data into *training* and *testing* partitions, we can "train" our **Classifier**.

GEE has a number of **Classifier** algorithms implemented:

- Maximum Entropy (``amnhMaxent``; `documentation <https://developers.google.com/earth-engine/apidocs/ee-classifier-amnhmaxent>`__)\ [1]_\ [2]_
- Support Vector Machine (``libsvm``; `documentation <https://developers.google.com/earth-engine/apidocs/ee-classifier-libsvm>`__)\ [3]_
- Minimum Distane (``minimumDistance``; `documentation <https://developers.google.com/earth-engine/apidocs/ee-classifier-minimumdistance>`__)\ [4]_
- CART (``smileCart``; `documentation <https://developers.google.com/earth-engine/apidocs/ee-classifier-smilecart>`__)\ [5]_
- Gradient Tree Boost (``smileGradientTreeBoost``; `documentation <https://developers.google.com/earth-engine/apidocs/ee-classifier-smilegradienttreeboost>`__)\ [6]_
- Naive Bayes (``smileNaiveBayes``; `documentation <https://developers.google.com/earth-engine/apidocs/ee-classifier-smilenaivebayes>`__)\ [7]_
- Random Forest (``smileRandomForest``; `documentation <https://developers.google.com/earth-engine/apidocs/ee-classifier-smilerandomforest>`__)\ [8]_

In this example, we're using ``ee.Classifier.smileRandomForest()`` to do a Random Forest classification.

.. code-block:: javascript

    var classifier = ee.Classifier.smileRandomForest(100).train({
      features: trainingPartition,
      classProperty: 'landcover',
      inputProperties: bands
    });

this will initialize a Random Forest **Classifier** with 100 trees, then use ``ee.Classifier.train()``
(`documentation <https://developers.google.com/earth-engine/apidocs/ee-classifier-train>`__) to train 
the classifier. The inputs to ``ee.Classifier.train()`` used above are:

- ``features``, the **FeatureCollection** to use to train the **Classifier**
- ``classProperty``, the property of ``features`` that contains the classification information
- ``inputProperties``, a list of the properties from ``features`` to use to train the **Classifier**

So, this will train the **Classifier** using the ``trainingPartition`` **FeatureCollection**,
based on the ``'landcover'`` property, using the image bands listed in ``bands``.


accuracy assessment
---------------------

Once we've trained the classifier, we can use the *testing* dataset to evaluate how accurate it is. First, we
have to use ``ee.FeatureCollection.classify()``
(`documentation <https://developers.google.com/earth-engine/apidocs/ee-featurecollection-classify>`__) to classify
the testing data:

.. code-block:: javascript

    var test = testingPartition.classify(classifier);

Next, we can create a "confusion matrix" to display how many of the training objects were
correctly or incorrectly classified as each object:

.. code-block:: javascript

    var cm = test.errorMatrix('landcover', 'classification');

This uses ``ee.FeatureCollection.errorMatrix()``
(`documentation <https://developers.google.com/earth-engine/apidocs/ee-featurecollection-errormatrix>`__) to create a
**ConfusionMatrix** object (`documentation <https://developers.google.com/earth-engine/apidocs/ee-confusionmatrix>`__).

The following line:

.. code-block:: javascript

    print('confusion matrix: ', cm,
      'overall accuracy: ', cm.accuracy(),
      'kappa: ', cm.kappa(),
      "producer's accuracy:", cm.producersAccuracy(),
      "consumer's accuracy:", cm.consumersAccuracy());

will print the **ConfusionMatrix** object, along with the *overall accuracy*, *kappa* score, *producer's* accuracy,
and *consumer's* accuracy to the **Console**:

- the *overall* accuracy is the number of correctly classified **Feature**\ s, divided by the total number of **Feature**\ s
- the *producer's* accuracy is the probability that a particular class is correctly classified, and it's the number of correctly classified **Feature**\ s divided by the total number of **Feature**\s in each row of the **ConfusionMatrix**.
- the *consumer's* accuracy is the probability that the map classification is correct, and it's the number of correctly classified **Feature**\ s divided by the total number of **Feature**\s in each column of the **ConfusionMatrix**.

.. note::

    The documentation for ``ee.ConfusionMatrix.producersAccuracy()`` and ``ee.ConfusionMatrix.consumersAccuracy()``
    appears to be incorrect - that is, based on the example code provided, ``ee.ConfusionMatrix.producersAccuracy()``
    uses the values in each *row* of the sample **Array**, while ``ee.ConfusionMatrix.consumersAccuracy()`` uses the
    values in each *column*.

The *kappa* score, or statistic, is calculated as follows:

.. math::

    \kappa = \frac{p_o - p_e}{1 - p_e}

where :math:`p_o` is the observed accuracy of the classifier, and :math:`p_e` is the hypothetical probability of chance agreement.
The *kappa* score thus gives a measure of how much better the classifier performs than would be expected by random chance.

When you run the script, you should see the following in the **console** panels (remember that your results may differ slightly):

.. image:: ../../../img/egm702/week5/error_matrix.png
    :width: 400
    :align: center
    :alt: the error matrix and accuracy values for the 100-tree random forest classification

To help you understand this, I've added row/column labels to this table below:

+----------------+-------+--------+-----------+------------+-----------+
|                | water | forest | grassland | built-up   | bare soil |
+================+=======+========+===========+============+===========+
| **water**      | 15    | 0      | 0         | 0          | 0         |
+----------------+-------+--------+-----------+------------+-----------+
| **forest**     | 0     | 13     | 0         | 0          | 0         |
+----------------+-------+--------+-----------+------------+-----------+
| **grassland**  | 0     | 0      | 9         | 0          | 1         |
+----------------+-------+--------+-----------+------------+-----------+
| **built-up**   | 0     | 0      | 0         | 8          | 2         |
+----------------+-------+--------+-----------+------------+-----------+
| **bare soil**  | 0     | 0      | 0         | 4          | 8         |
+----------------+-------+--------+-----------+------------+-----------+

The "rows" of this matrix correspond to the landcover class that we have identified,
while the columns correspond to the classified values. In the example above, we see that 15 of our training samples
were classified as landcover class 0 (water), and there were no water training samples that were classified as
something else. The same is true for the forest class (value 1), while one grassland **Feature** (value 2) was
classified as bare soil.

Of the 10 built-up **Feature**\ s in our testing dataset, 8 were correctly classified, while 2 were mis-classified as
bare soil.

Four bare soil **Feature**\ s were mis-classified as built-up areas, and the remaining 8 were correctly
classified as bare soil.

From this example, we can also see that the overall accuracy is decently high (88.3%), with a reasonably high
kappa statistic (0.853).

The *producer's* accuracy is similarly high for each class except for bare soil, where 4 of the 12 test **Feature**\ s
were misclassified.

+---------------+-----------------------+-----------------------+
| class         | producer's accuracy   | consumer's accuracy   |
+===============+=======================+=======================+
| **water**     | 15/15 = 100%          | 15/15 = 100%          |
+---------------+-----------------------+-----------------------+
| **forest**    | 13/13 = 100%          | 13/13 = 100%          |
+---------------+-----------------------+-----------------------+
| **grassland** | 9/10 = 90%            | 9/9 = 100%            |
+---------------+-----------------------+-----------------------+
| **built-up**  | 8/10 = 80%            | 8/12 = 66.7%          |
+---------------+-----------------------+-----------------------+
| **bare soil** | 8/12 = 66.7%          | 8/11 = 72.7%          |
+---------------+-----------------------+-----------------------+

While these are encouraging results, it's worth keeping in mind that

classifying the image
----------------------

.. code-block:: javascript

    var classified = img.select(bands).classify(classifier);



examining the results
----------------------

spectral signatures
.......................


landcover area by class
........................


next steps
-----------

- how does changing the number of 'trees' in the random forest classifier impact the estimated accuracy of the classification? 
- try a different classifier
- additional bands? NDVI, NDWI, etc.
- clouds

references
------------

.. [1] This particular implementation is the American Museum of Natural History (AMNH) maximum-entropy classifier; for more information about the software, see https://biodiversityinformatics.amnh.org/open_source/maxent/

.. [2] e.g., De Martino, A. and D. De Martino (2018). *Heliyon*, 4(**4**), e00596. doi: `10.1016/j.heliyon.2018.e00596 <https://doi.org/10.1016/j.heliyon.2018.e00596>`__

.. [3] e.g., Mountrakis, G., et al. (2011). *ISPRS J. Photogramm. Rem. Sens.* 66, 247–259. doi: `10.1016/j.isprsjprs.2010.11.001 <https://doi.org/10.1016/j.isprsjprs.2010.11.001>`__

.. [4] e.g., Wacker, A. G. and D. A. Landgrebe (1972). *LARS Technical Reports*. Paper 25. http://docs.lib.purdue.edu/larstech/25

.. [5] e.g., 

.. [6] e.g., 

.. [7] e.g., 

.. [8] e.g., 

