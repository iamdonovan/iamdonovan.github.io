interaction with earth's surface
=================================

definitions
------------

Before we jump fully into looking at how electromagnetic radiation interacts with objects, we need to have some
definitions, because they will come up again and again:

- **Radiant energy** (:math:`Q`, [J]): the total amount of energy emitted by, or falling on, an object.
- **Radiant flux** (:math:`\Phi`, [W] [J s\ :sup:`-1`]): total amount of energy emitted by, or falling on, an object
  per unit time
- **Radiant intensity** (:math:`I`, [W sr\ :sup:`-1`]): radiant flux per
  `solid angle <https://en.wikipedia.org/wiki/Solid_angle>`__
- **Radiance** (:math:`L`, [W sr\ :sup:`-1` m\ :sup:`-2`]): flux per solid angle per area that is emitted by, or falls
  on, an object.
- **Radiant emittance** (:math:`M`, [W m\ :sup:`-2`]): the total radiant flux emitted from a surface
- **Irradiance** (:math:`E`, [W m\ :sup:`-2`]): the total radiant flux onto a surface
- **Radiosity** (:math:`J`, [W m\ :sup:`-2`]): the total radiant flux leaving a surface (i.e., the sum of the flux that
  is emitted, reflected, and transmitted)
- **Spectral radiance** (:math:`L_\lambda`, [W sr\ :sup:`-1` m\ :sup:`-3`]): Radiance per wavelength unit
- **Spectral irradiance** (:math:`E_\lambda`, [W m\ :sup:`-3`]): Irradiance per wavelength unit

Similar to what we discussed for the atmosphere, electromagnetic radiation interacts with the Earth’s surface by
either being reflected, absorbed, or transmitted:

**interaction diagram**

|br| How it interacts with the surface depends on the properties of the surface, the wavelength of the light, and the
angle of illumination, or incidence.

It’s important to note that these are not mutually exclusive – an object can transmit some incident radiation, absorb
some, and reflect the rest – or, it can completely absorb, or completely reflect, the incident radiation. In any case,
the incident radiant flux, :math:`\Phi_i`, is the sum of the radiant flux that is reflected (:math:`\Phi_r`),
absorbed (:math:`\Phi_a`), and transmitted (:math:`\Phi_t`):

.. math::

    \Phi_i = \Phi_r + \Phi_a + \Phi_t

reflection
-----------

For most of the remote sensing we’ll talk about in the rest of this module, reflection is the main type of surface
interaction we’re interested in. This is usually what we measure with optical – that is, visible or infrared – sensors.

The image below shows how much energy has reflected off the Earth’s surface towards the satellite in the
near-infrared portion of the spectrum (remember that these are wavelengths around 900 nm):

.. image:: img/reflectance_example.png
    :width: 500
    :align: center
    :alt: a black and white satellite image showing a mountainous area covered by snow and glaciers

|br| In general, we can break surfaces into two idealized types based on how they reflect electromagnetic radiation:
specular, or mirror-like reflectors, and diffuse, or Lambertian, reflectors.

We can also define the **reflectance**, :math:`\rho`, of an object as the ratio of the energy reflected by the
surface to the energy incident on the surface:

.. math::

    \rho = \frac{E_r}{E_I}

In other words, this is the fraction of energy incident on the surface that is reflected by the object. In the image
above, areas that appear white (snow and ice in the example) have a high reflectance - more energy is reflected by the
surface and recorded by the sensor, at least at this particular wavelength. Darker areas have lower reflectance - more
of the incoming energy is either absorbed by the surface, or it is reflected away from the sensor, or it is transmitted
through the surface.


specular reflectors
^^^^^^^^^^^^^^^^^^^^^

Specular, or "mirror-like" reflectors, are surfaces that are smooth relative to the wavelength of the electromagnetic
radiation. Similar to a mirror, or a perfectly calm lake surface, perfect specular reflectors re-direct, or reflect,
nearly all of the incident radiation in a single direction.


For a perfect specular reflector, the angle of reflection, or exitance, is equal to the angle of incidence:

**reflector diagram**

|br| Most surfaces are not perfect specular reflectors, however, so there may be some light scattered in other
directions – in this case, most of the radiation, rather than all of the radiation, is reflected at an angle equal
to the angle of incidence.

diffuse reflectors
^^^^^^^^^^^^^^^^^^^^^

Diffuse reflectors are surfaces that are **rough** relative to the wavelength of the electromagnetic radiation, which
means that energy is scattered in many different directions:

**diffuse diagram**

In the case of a perfect diffuse reflector, known as a Lambertian surface, the incident radiation is scattered
uniformly in all directions. Similar to non-perfect specular reflectors, non-perfect diffuse reflectors have some
preferential scattering at an angle equal to the angle of incidence, but more of the radiation is scattered from
the surface.

Because of the way that the electromagnetic radiation interacts with the surface, diffuse reflection actually tells us
about the color of the surface. Some wavelengths are absorbed by the surface, and anything not absorbed is reflected
by the surface. Because of this, diffuse reflection is often the most useful type of reflection for remote sensing,
because it enables us to distinguish objects based on the wavelengths of reflected light.


the bi-directional reflectance distribution function (brdf)
------------------------------------------------------------

Most surfaces lie somewhere between the idealized surface types of specular reflectors and diffuse reflectors. And, in
fact, whether surfaces behave more like specular or more like diffuse reflectors normally depends on the viewing angle.

For example, in these two images, you can see the arrow pointing to water on the ocean:

.. image:: img/brdf_example.png
    :width: 600
    :align: center
    :alt: two black and white satellite images, demonstrating that reflectance depends in part on viewing angle

|br| Notice how bright the water appears in the image on the left, compared to the image on the right. In the image on
the left, the sensor (in this case, a camera) is picking up a strong reflection of the sun’s light off of the water
surface. When the camera moves to its next position (the image on the right), the same area appears dark – the
reflection from the surface is no longer pointing directly at the sensor.

One way that we can describe or assess this tendency of a surface’s reflectance is something called the bidrectional
reflectance distribution function (BRDF). The BRDF is a mathematical description of how the reflectance varies for
combinations of illumination and reflection angles at a given wavelength.

Given the BRDF of a surface, we can estimate its albedo – the ratio of the radiosity, or total radiant flux leaving a
surface, to the irradiance, or total radiant flux onto a surface. Albedo is an important concept for climate, as it in
part helps to determine the energy balance of Earth’s surface.

In order to estimate the BRDF and the albedo, we need multiple viewing angles of the surface. This last image here is
of the satellite Terra, and it demonstrates how a sensor called the Multi-angle Imaging SpectroRadiometer (MISR) works:

**misr**

|br| MISR has nine different cameras, each acquiring images at different angles. With measurements like this, we can
work out the BRDF and albedo for objects and surfaces all over the Earth.


absorption and transmission
----------------------------

Any energy that isn’t reflected by a surface has to be either absorbed or emitted by the surface. We covered this a
bit with diffuse reflectors – the properties of the surface determine how electromagnetic radiation is absorbed, and
at what wavelengths. For example, leaves on healthy, chlorophyll-producing plants absorb light in the red and blue
visible wavelengths, leaving mostly green light to be reflected – as a result, most plants appear green to our eyes.
We can also see absorption and transmission in action with the color of water. At the shore of the lake here, water is
mostly clear. As the depth increases, though, we see a shift in color to green and then dark blue. Water molecules
preferentially absorb longer wavelengths like red light, so the light that gets scattered back toward the sensor is at
shorter wavelengths. As the water gets deeper, more of the light is absorbed, and so the water appears darker and
darker – less of it is reflected back. Scattering by suspended sediments and other particles in the water also plays
a role – because most of the light that is transmitted into the water column is preferentially shorter wavelengths,
the light scattered back appears more green and blue, depending again on the depth.



additional reading
-------------------

