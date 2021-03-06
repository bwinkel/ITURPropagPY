ITURPropagPy
============

|GitHub license| |Build Status| |PyPI version| |Coverage Status|

A python implementation of the ITU-R P. Recommendations to compute
atmospheric attenuation in slant and horizontal paths.

The propagation loss on an Earth-space path and a horizontal-path,
relative to the free-space loss, is the sum of different contributions,
namely: attenuation by atmospheric gases; attenuation by rain, other
precipitation and clouds; scintillation and multipath effects;
attenuation by sand and dust storms. Each of these contributions has its
own characteristics as a function of frequency, geographic location and
elevation angle. ITU-Rpy allows for fast, vectorial computation of the
different contributions to the atmospheric attenuation.

Documentation
-------------

The documentation can be found at [<https://github.com/mrazavian/ITURPropagPY/tree/master/Documents>].

Examples of use cases can be found in the
[<https://github.com/mrazavian/ITURPropagPY/tree/master/Examples>]

Installation
------------

ITU-RPropagpy has the followind dependencies: ``numpy``, ``scipy``,
``joblib``, ``pyproj``, ``h5py``, and ``astropy``. Installation of ``basemap`` and
``matplotlib`` is recommended to display results in a map.

Using pip , you can install all of them by running:

::

    pip install git+https://github.com/mrazavian/ITURPropagPY

More information about the installation process can be found on the
[<https://github.com/mrazavian/ITURPropagPY>].

ITU-R Recommendations implemented
----------------------------------

The following ITU-R Recommendations are implemented in ITURPropagPY

* **ITU-R P.453-13:** The radio refractive index: its formula and refractivity data
* **ITU-R P.618-13:** Propagation data and prediction methods required for the design of Earth-space telecommunication systems
* **ITU-R P.676-11:** Attenuation by atmospheric gases
* **ITU-R P.835-6:** Reference Standard Atmospheres
* **ITU-R P.836-6:** Water vapour: surface density and total columnar content
* **ITU-R P.837-7:** Characteristics of precipitation for propagation modelling
* **ITU-R P.838-3:** Specific attenuation model for rain for use in prediction methods
* **ITU-R P.839-4:** Rain height model for prediction methods.
* **ITU-R P.840-7:** Attenuation due to clouds and fog
* **ITU-R P.1144-7:** Interpolation methods for the geophysical properties used to compute propagation effects
* **ITU-R P.1511-2:** Topography for Earth-to-space propagation modelling
* **ITU-R P.1853-2:** Tropospheric attenuation time series synthesis

The individual models can be accessed using the ``iturpropag.models`` package.

Usage
-----

The following code example shows the usage of ITURPropagPY. More examples can
be found in the [<https://github.com/mrazavian/ITURPropagPY/tree/master/Examples>].

.. code:: python

    import matplotlib.pyplot as plt
    import iturpropag

    f = 22.5 * iturpropag.u.GHz    # Link frequency
    D = 1 * iturpropag.u.m         # Size of the receiver antenna
    el = 60                  # Elevation angle constant of 60 degrees
    p = 3                    # Percentage of time that attenuation values are exceeded.
    tau = 45
    eta = 0.6

    # Generate a regular grid latitude and longitude points with 1 degrees resolution   
    lat, lon = iturpropag.utils.regular_lat_lon_grid() 

    # Comute the atmospheric attenuation
    Att = iturpropag.atmospheric_attenuation_slant_path(lat, lon, f, el, p, D, tau, eta) 
    iturpropag.utils.plot_in_map(Att.value, lat, lon, 
                           cbar_text='Atmospheric attenuation [dB]')
    plt.show()

which produces:

![alt "atmospheric attenuation"](https://i.pinimg.com/originals/cd/b2/7c/cdb27cd40c6c3af9f53df739c744d746.png "Atmospheric Attenuation")

Citation
--------

If you use ITURPropagPY in one of your research projects, please cite it as:

::

    @misc{iturpropagpy-2019,
          title={ITURPropagPY: A python implementation of the ITU-R P. Recommendations to compute atmospheric attenuation in slant and horizontal paths.},
          author={Inigo del Portillo, Mojtaba Razavian, Thomas A. Prechtl},
          year={2019},
          publisher={GitHub},
          howpublished={\url{https://github.com/mrazavian/ITURPropagPY}}
    }

Keywords: atmopheric-propagation attenuation communications
Platform: UNKNOWN
Classifier: Development Status :: 3 - Alpha
Classifier: Intended Audience :: Telecommunications Industry
Classifier: Topic :: Scientific/Engineering :: Physics
Classifier: License :: OSI Approved :: ESA-PL – v2.3
Classifier: Programming Language :: Python :: 2
Classifier: Programming Language :: Python :: 2.7
Classifier: Programming Language :: Python :: 3
Classifier: Programming Language :: Python :: 3.4
Classifier: Programming Language :: Python :: 3.5
Classifier: Programming Language :: Python :: 3.6
Classifier: Programming Language :: Python :: 3.7
