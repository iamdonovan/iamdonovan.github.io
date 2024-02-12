electromagnetic radiation
===========================

When we defined remote sensing, we also noted that in a way, we've all been doing remote sensing for years. Our eyes,
ears, and nose all collect data about the world without touching it - they are remote sensors. In particular, our eyes
use light in order to sense the world around us – in a very similar way to how we collect remote sensing data.

The light that we see with our eyes is a type of **electromagnetic radiation**. For most remote sensing, we use
electromagnetic radiation to observe things. But, how should we think about, or picture, light (or electromagnetic
radiation)?

For the kind of remote sensing we're covering here, we use electromagnetic radiation to observe things. But, how
should we think about light (or electromagnetic radiation)?

Over time, physicists developed two main theories for how light behaved: the **particle model** and the **wave model**,
based on different phenomena or properties they observed. If we make a table of the different properties of
electromagnetic radiation, we can see how neither model manages to explain all of the different properties:

.. csv-table:: Properties of light explained by different models of light
    :header: , particle, wave

    reflection, :fas:`check`, :fas:`check`
    refraction, :fas:`check`, :fas:`check`
    interference, :fas:`xmark`, :fas:`check`
    diffraction, :fas:`xmark`, :fas:`check`
    polarization, :fas:`xmark`, :fas:`check`
    `the photoelectric effect <https://www.youtube.com/watch?v=v-1zjdUTu0o>`__, :fas:`check`, :fas:`xmark`

Both models can explain reflection and refraction, but only the wave model can explain the properties of interference,
diffraction, and polarization. But, the wave model can’t explain the photoelectric effect, whereas the particle model can.

So, the answer to the question "is light a particle or a wave?" is "it depends." The reason why this is the case is
well outside of the scope of this course, but if you’re interested there are more links in the notes section that go
deeper into the topic.


the wave model
---------------

In the wave model, electromagnetic radiation is a **self-propagating wave**. By "self-propagating" we mean that, unlike
water waves or sound waves, electromagnetic waves travel through space without any external influence.

As the name suggests, electromagnetic waves have both an electric component and a magnetic component. One of the
`major lessons <https://en.wikipedia.org/wiki/Faraday%27s_law_of_induction>`__ of 19th-century physics is that a
changing electric field induces a magnetic field, and vice-versa. This is the principle behind, among other things,
induction stovetops and electric motors.

So an electromagnetic wave moving through space has both an electric and a magnetic component, usually denoted **E**
(colored blue in the diagram below) and **B** (red), respectively:

.. image:: img/emr_wave.png
    :width: 720
    :align: center
    :alt: a diagram of an electromagnetic wave, with the electric component colored blue and the magnetic
        component shaded red

The electric component is moving and oscillating in one plane – in this example, the *xz* plane, while the
magnetic component moves and oscillates in a plane at a 90-degree angle – in this example, the *xy* plane.

Like any other wave, an electromagnetic wave has different attributes, or properties. It propagates at a certain speed,
usually denoted :math:`c`. In a vacuum, the speed of light is about :math:`3\times 10^8` m s\ :sup:`-1`. In other
materials, such as Earth's atmosphere, it drops by about 90 km/s – about .03% slower.

The **wavelength** of an electromagnetic wave, :math:`\lambda`, is defined as the distance between one full cycle
of the wave. This can be measured between successive peaks as shown above, between successive "troughs", or even the
distance between points where the electric component is 0.

Another important property is the frequency, usually denoted :math:`f` or :math:`\nu`, of the
wave. This is the amount of time it takes to go through a single cycle. The wavelength and frequency of a wave are both
related to the speed of the wave, :math:`c`, according to this equation:

.. math::

    c = \lambda f

Other properties of electromagnetic waves include the **phase**, or the fraction of a cycle, usually denoted as
:math:`\phi`. As you might have guessed, this is usually defined between 0 and 2\ :math:`\pi`, or 0 and 360 degrees.

Finally, there’s the **amplitude** (:math:`A`) of the wave, which is the height of the peak or the depth of the trough,
and this is associated with the brightness or intensity of the light.

The table below lists the different properties of the wave, and their respective units.

.. csv-table:: Properties of the wave model and corresponding units
    :header: name, symbol, units

    speed, :math:`c`, m s\ :sup:`-1`
    wavelength, :math:`\lambda`, m
    frequency, :math:`f` or :math:`\nu`, s\ :sup:`-1` (Hz)
    phase, :math:`\phi`, radians or degrees

Light/electromagnetic radiation is a *transverse wave* – that is, the electric and magnetic components of the wave
oscillate perpendicular to the direction of motion. We can therefore define, or specify, an orientation for this
oscillation, called the polarization of the wave. By convention, we normally define the polarization using the electric
component of the wave.

The figure below shows an example of two different polarizations of a light wave:

.. image:: img/emr_wave_vpol.png
    :width: 49%
    :alt: a diagram illustrating a vertically-polarized light wave

.. image:: img/emr_wave_hpol.png
    :width: 49%
    :alt: a diagram illustrating a horizontally-polarized light wave


|br| In the example on the left, the wave is vertically polarized: the electric field (in blue) is oriented along the
*x*-axis, in the *xz*-plane. In the example on the right, the electric field is still propagating along the *x*-axis,
but it is oscillating in the *xy*-plane – we would say that this is horizontally polarized.

Light can be polarized at any arbitrary angle – it can even have a circular or elliptical polarization, where the plane
is rotating around the direction of motion:

**elliptical polarization**

|br| Because of this, we can actually construct filters that will only allow through light at a specified polarization. This
is especially useful for radar remote sensing, where the polarization of the radar signal partly determines what we
actually "see" with the signal. We can also use this to create glare-reducing polarized sunglasses.


the particle model
-------------------
Remember that light, or electromagnetic radiation, can behave as both a particle and a wave. We’ve seen how we can
describe light as a wave, and now we’ll take a look at the particle model.

In this model, light is a particle, called a **photon**, that has a particular energy :math:`Q`. Another
of the big discoveries of 19th and early 20th century physics is that objects (that is, atoms), can only absorb
and emit energy in discrete units, called **quanta**, or photons. This is where we get the term "quantum mechanics".

The amount of energy, then, that a photon has is directly related to its frequency:

.. math::

    Q = hf

where :math:`h = 6.62607015\times 10^{-34}` J Hz\ :sup:`-1` is a constant called **Planck’s constant**.

Using what we know about the relationship between the frequency and wavelength of light, then, we can re-write this:

.. math::

    Q = \frac{hc}{\lambda},

The table here lists the properties of the particle, and the different units:

.. csv-table:: Properties of the particle model and corresponding units
    :header: name, symbol, units

    energy, Q, Joules [J]
    Planck's constant, :math:`h`, [J\ :math:`\cdot`\ s]
    frequency, :math:`f` or :math:`\nu`, s\ :sup:`-1` (Hz)

From the equation above, we can see that the energy contained in a photon is inversely proportional to its wavelength.
Or, put another way, longer wavelengths mean lower frequencies mean lower energy. And, conversely, shorter wavelengths
mean higher frequencies mean higher energy.

For remote sensing, this also means that longer wavelengths are harder to detect: we need more photons at lower
energies to strike our sensor in order to register a signal, compared to higher-energy photons. One big consequence
of this is that that sensors that detect longer wavelengths typically have a lower resolution compared to sensors that
detect shorter wavelengths. This has implications for forms of passive remote sensing such as thermal or passive remote
sensing, which typically use very long wavelengths (:math:`\lambda > 10000` nm).


blackbody radiation
--------------------

All matter that has a temperature above 0 K (-273.15°C) emits electromagnetic radiation. The amount of radiation that
is emitted, also called the **radiant emittance**, strongly depends on the temperature.

For an idealized object, called a **blackbody**, that perfectly absorbs and re-emits all of the energy that falls on it,
the radiant emittance :math:`M` is directly proportional to its temperature, :math:`T` raised to the fourth power:
**Stefan-Boltzmann law**:

.. math::

    M = \sigma T^4

where :math:`\sigma` is the **Stefan-Boltzmann constant**. This equation tells us that small increases in temperature
lead to large increases in radiant emittance.

In reality, most objects aren’t perfect blackbodies – instead, they emit some fraction of the electromagnetic radiation
that blackbodies do. We can measure how well an object approximates a perfect blackbody via its **emissivity**,
:math:`\varepsilon`, which is defined as the ratio of its emittance :math:`M` to the emittance of a blackbody with the
same temperature, :math:`M_b`:

.. math::

    \varepsilon = \frac{M}{M_b}


.. csv-table::
    :header: name, symbol, units

    radiant emittance, :math:`M`, W m\ :sup:`-2`
    Stefan-Boltzmann constant, :math:`\sigma`, W m\ :sup:`-2` K\ :sup:`-4`
    temperature, :math:`T`, K

planck's law
-------------

Putting all of this together, we see that objects with higher temperature have higher energy. This means that the
electromagnetic radiation they emit will have a higher frequency, or a shorter wavelength.
**Planck's Law of Blackbody Radiation** tells us the **spectral radiance** :math:`L_\lambda` (the amount of energy
that a blackbody emits per unit frequency/wavelength) for a blackbody at a given temperature, :math:`T`:

.. math::

    L(\lambda, T) = \frac{2 h c^2}{\lambda^5} \left(\frac{1}{e^{hc/\lambda k T} - 1}\right),

Here, we see that :math:`L` is a function of wavelength, :math:`L` and temperature, :math:`T`. :math:`k` is the
*Boltzmann constant* (:math:`k = 1.380649\times 10^{−23}` J K\ :sup:`−1`), :math:`h` is Planck's constant, and :math:`c`
is the speed of light in a vacuum.

Planck's law tells us that objects with a higher temperature will emit more electromagnetic radiation at higher
frequencies/shorter wavelengths:

.. image:: img/planck_plot.png
    :width: 500
    :align: center
    :alt: a plot showing the radiance emitted at a given wavelength for blackbodies at a range of temperatures

|br| The plot here shows how an object’s radiance (amount of energy emitted) varies with both wavelength and
temperature. Note that this is a semi-logarithmic plot – the steps on the *y*-axis represent an increase of 1000, while
the steps on the *x*-axis go from 100, to 1000, to 10000, and so on.

Cooler objects, shown as darker lines on the plot, have lower overall radiance, and the wavelengths they emit most
at are much longer. As we increase in temperature, we also increase the overall radiance: the peak gets higher and
higher, and we shift the peak of the curve toward lower wavelengths.

In space, our sun appears mostly white because it emits fairly evenly across the wavelengths that we can see with our
eyes, though our atmosphere changes this slightly. Wood fires with a temperature of around 1500 K appear mostly
reddish-orange to our eyes, while the human body at ~300K doesn’t really emit at all in the wavelengths our eyes can see.

We can calculate the dominant wavelength that an object emits, :math:`\lambda_{\rm peak}` (i.e., the color of its
maximum radiance), using something called Wien’s displacement law:

.. math::

    \lambda_{\rm peak} = \frac{b}{T},

where :math:`b` is *Wien's displacement constant* (:math:`\approx` 2898 µm K).

So, for example, a human body at approximately 300K has a peak wavelength of 9.66 µm or 9660 nm. The sun, with a
surface temperature of around 6000K, has a peak wavelength of 0.483 µm (483 nm).

the electromagnetic spectrum
------------------------------

Electromagnetic radiation comes in a large range of possible wavelengths or frequencies, which we call the
**electromagnetic spectrum**. We can somewhat arbitrarily divide the spectrum into regions of wavelengths with
"similar enough" properties:

**em spectrum**

|br| As you can see here, the light that we can see with our eyes, known as visible light or visible electromagnetic
radiation, makes up a very small portion of the electromagnetic spectrum, with wavelengths between about 400 and 700 nm.

Just below visible light we have ultraviolet light, with wavelengths between about 10 and 400 nm. Above the visible
spectrum we have infrared light, followed by microwaves and then radio waves, which can have wavelengths over several
km. Each of these different regions has its own properties that we can use to study different things.

The divisions are somewhat arbitrary, and different users may have different definitions, or different preferred units.
Electrical engineers and people who do microwave remote sensing tend to prefer Herz (Hz, units of frequency), while
people who do optical/thermal remote sensing tend to prefer wavelength units.

The table below lists a number of different portions of the electromagnetic spectrum that we often use for remote
sensing – you can look this over and see the different definitions here.

.. csv-table:: Different regions and wavelength ranges used in remote sensing
    :header: region, limits

    **visible light**, **380--720 nm**
    blue, 400--500 nm
    green, 500--600 nm
    red, 600--700 nm
    **infrared**, **700--10**\ :sup:`6` **nm (1 mm)**
    near-infrared, 700--1000 nm
    shortwave infrared, 1000--3000 nm
    mid infrared, 3000--8000 nm
    longwave infrared, 8000--14000 nm
    far infrared, 14000--10\ :sup:`6` nm
    **microwave**, **1 mm -- 1 m**

.. card::
    :class-header: question
    :class-card: question

    :far:`circle-question` Question
    ^^^

    Why do you think that I haven’t listed any wavelengths shorter than visible light in the above table?


additional reading
-------------------

- Lillesand, Kiefer and Chipman, Chapter 1, 4.8--4.11
- Campbell & Wynne, Chapter 2, 9
- Tour of the Electromagnetic Spectrum [`NASA <https://www.youtube.com/watch?v=lwfJPc-rSXw&list=PL09E558656CA5DF76>`__]
- EM waves and the EM spectrum [`Khan Academy <https://www.youtube.com/watch?v=7eutept5h0Q>`__]
- The photoelectric effect [`National STEM Centre <https://www.youtube.com/watch?v=v-1zjdUTu0o>`__]
- The Ultraviolet Catastrophe [`Physics Girl <https://www.youtube.com/watch?v=FXfrncRey-4>`__]