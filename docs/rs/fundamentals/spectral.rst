spectral properties
====================

Recall from the last lesson that the reflectance of an object, or the ratio of the energy that it reflects to the
energy that falls on it, depends on its surface properties such as its roughness. It also depends on the chemical
composition, or what molecules make up the surface, but also the viewing angle and angle of illumination.

We talked about two examples: how healthy, chlorophyll-producing plants appear green because they absorb red and blue
wavelengths of light, reflecting green wavelengths; and how water preferentially absorbs longer wavelengths, causing it
to look bluer and bluer as it gets deeper.

All of this is to say – objects or surfaces reflect differently at different wavelengths.

definitions
------------

Before we start, we have to lay out some definitions:

- the **spectral reflectance** of an object or a surface, :math:`\rho_\lambda`, is the reflectance of an object for a
  given wavelength, :math:`\lambda`. This is similar to how we defined the spectral radiance or irradiance of an object
  as the radiance or irradiance for a given wavelength.
- The **spectral signature** of an object or surface is just the pattern of spectral reflectance across the
  electromagnetic spectrum.
- We can display an object’s spectral signature as a **spectral response curve**, several examples of which are shown
  below:

**spectral curves**

|br| We see here that in the visible wavelengths, these different plants, oak, lawn grass, and conifer, all have similar
spectral signatures, just perhaps at different brightness levels. But, the plants all look quite different to the
concrete, or the snow, which have somewhat similar reflectances across red, green, and blue wavelengths.

Moving into the infrared wavelengths, we see that concrete has a fairly even reflection, while the pattern of our
different vegetation types is quite distinctive. We can also see that water has a pretty low reflection across the
electromagnetic spectrum. We can use spectral signatures to help differentiate between surfaces and objects, potentially
allowing us to map things like vegetation, or snow, or water bodies, or anything else we might be interested in.


measuring spectral properties
------------------------------

In order to use the spectral properties of different objects, though, we have to measure them. In the field, or in the
lab, we use an instrument called a spectrometer. A spectrometer, seen here in action somewhere in Arizona, takes the
incoming light and breaks it into its individual spectral components, similar to how a prism works. It then records
the reflectance of the object at those different wavelengths – in other words, it records a bunch of spectral
reflectances. We often need to take multiple measurements of multiple samples, as even the same material can have
variable spectral signatures – remember again that the amount of energy reflected depends on surface properties, as
well as illumination angle or viewing angle. Instead of a field spectrometer, we can also use a hyperspectral
camera – an instrument that records radiation in a large number of wavelengths. We can also use some satellite
images – some sensors record in a large number of wavelength ranges, or bands – if we know exactly what we’re looking
at in a given image, we can use this information to estimate the object’s spectral signature.


"true color" images
--------------------

From here, we’re going to look at the same image in a number of different ways. Obviously, this is an image showing a
portion of Northern Ireland – we have Derry/Londonderry here in the lower right, or southwest, portion of the image;
Lough Foyle is here, with Magilligan Point; Coleraine is here in the more eastern part of the image, and Portrush and
Portstewart here along the coast.

This image is what is known as a “true-color” or “natural color” image – it’s displayed with the red wavelengths
recorded by the sensor displayed as red on the computer screen; green wavelengths displayed as green; and blue
wavelengths displayed as blue. You can see also our spectral curve plot here in the corner, with the different bands
highlighted.

In this image, we see lots of green – no big surprise, as it was acquired in the summer months, with lots of
agricultural land and crops growing in the region, everything tends to be quite green. But we can also pick out some
other things – the cities and towns tend to look a bit more gray, there’s some darker bands of forest here in the
middle of the image, and we see some other patterns in the agricultural fields over here north of Limavady, which
might indicate different crops, or fields that haven’t been planted.

"false color" images
---------------------

If we then change the color combination to what is known as a false-color image, the image is now displayed so that
the near-infrared recorded by the sensor is displayed as red on the computer screen; red is displayed as green; and
green is displayed as blue. And what we can see is – everything has flipped from green to red. If you look at the
spectral curve over here, you can maybe understand why – the different vegetation types all have very high reflectance
in the near-infrared – much higher than in the red or the green, which means that the image appears red overall. We
can also see that the water appears mostly black, blue, or green – water reflects very little in the near-infrared, so
we don’t have any red coloring in this image. The cities we looked at before appear mostly blue-gray, indicating that
they’re fairly bright across the three bands, but maybe a bit higher in the green.


visible blue
-------------

Next, we’ll look at some single-band images – images corresponding to a single wavelength range. At the top of the
slide, I’ve indicated the wavelength range recorded by the sensor – here, it’s between 450 and 510 nm, corresponding
to visible blue light. You can see that the brightest parts of the image are along the coast on the nice white sand
beaches, in some of the fields we noted earlier, and in the cities. We can also see the different sediment patterns
in the Lough, indicating that there’s some transmission of blue light through the water.


visible green
--------------

Next up, we’re seeing the visible green wavelengths recorded by the sensor. You see that the land is much brighter here,
as the different plants we noted earlier reflect more radiation in green wavelengths.  We can also see the sediment
patterns in the Lough, but note that the bands of forest here in the middle of the scene are quite dark – remember
how they were very dark green in the true-color image – this indicates a much lower level of reflection from the trees
here than for the other types of vegetation we can see in the image.


visible red
------------

Moving on to the visible red wavelengths, we see how the agricultural lands we noted earlier are a bit darker. We can
still see the sediment patterns in the Lough, though they’re significantly darker than in the green and blue
wavelengths. Note that the cities haven’t changed significantly through the visible wavelengths – in the true-color
image, they were more of a gray color, indicating relatively even reflection in red, blue, and green wavelengths.

near infrared
--------------

In the near infrared, all of the vegetation that we saw earlier is extremely bright – note the large peaks for the
different vegetation types in the spectral curves. Note also that the Lough, where we could see sediment patterns
earlier, is completely black. Liquid water absorbs nearly all radiation in the near-infrared, and so there is very
little reflection or transmission.

Even the bands of forest that we saw earlier are quite bright, though not as bright as the other green plants. Finally,
the cities are somewhat darker than the vegetation, something we could also see in the false-color image, where the
cities all appeared blue-gray.

shortwave infrared: 1600 nm
----------------------------

In the shortwave infrared around 1600 nm, the water is still very dark, while the vegetation is still bright, though a
bit less bright than before. The exception is the bands of forest here in the middle of the image, which are again quite
dark. You can also see that the cities are still fairly bright, corresponding to the mostly flat curve for concrete
shown in the plot up here.


shortwave infrared: 2200 nm
----------------------------

Finally, in the shortwave infrared around 2200 nm, the picture looks fairly similar to 1600 nm, but a bit dimmer – you
can see from the spectral curves that most surfaces reflect a bit less as we move to longer wavelengths.





additional reading
-------------------

- Lillesand, Kiefer & Chipman - Chapter 1
- Campbell & Wynne - Chapter 2
- Mapping the Invisible [`NEON Science <https://www.youtube.com/watch?v=3iaFzafWJQE>`__]
- Landsat 8: Band by Band [`NASA <https://www.youtube.com/watch?v=A6WzAc1FTeA>`__]
