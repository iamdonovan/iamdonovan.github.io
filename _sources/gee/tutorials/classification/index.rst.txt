image classification 
=====================

Remotely-sensed imagery can be difficult to interpret for a number of reasons. The ultimate goal in remote sensing is to derive
information from the raw image data - that is, we want to identify, or *classify*, what we see in the image.

Because identifying each pixel by hand (or even large groups of pixels) is tedious and time-consuming, we want to try to avoid this
as much as possible, at least on a large scale. For that, we turn to (semi) automated *classification*, so that we can get the
computer to do as much of the work for us as possible.

In general, we can characterize classifications in a few different ways; for these tutorials, we focus on three:

- *unsupervised* classification, where we have nearly no input into how the computer classifies pixels;
- (supervised) *pixel-based* classification, where individual pixels are classified based on input data;
- (supervised) *object-based* classification, where pixels are grouped together before being classified based on input data.

.. toctree::
   :glob:
   :maxdepth: 1

   unsupervised
   pixel
   obia

