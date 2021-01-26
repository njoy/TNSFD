.. _theory:

=====================================
Theory 
=====================================




--------------------
Thermal Neutrons 
--------------------

The scattering cross sections of resonance-range and fast neutrons are typically considered not to be functions of the scattering material's molecular structure. And for these sufficiently fast neutrons, neglecting molecular structure is a valid approximation. When an incoming neutron has energy greater than a few eV, then the material's bonds are relatively insignificant and the scattering event could be considered to occur off an unbound atom. 

For thermal neutrons (i.e. neutrons with energy on the order of a few eV or less), the effects of material structure cannot be so readily dismissed. Thermal neutrons have energy comparable to the material's vibrational, translational, and rotational modes (vibrational modes being of particular interest here). Thus, during a thermal neutron scatters event, the neutron may excite/de-excite one or more of the material's vibrational modes, which dictates the outgoing neutron energy. 






.. _inelastic_scattering:

-------------------------------
Inelastic Scattering 
-------------------------------

Inelastic thermal neutron scattering involves a neutron changing energy via the creation or destruction of vibrational modes, called phonons. To describe such events, LEAPR prepares the **scattering law** :math:`S(\alpha,\beta)`, which is a function of unitless momentum change :math:`\alpha` and unitless energy change :math:`\beta`. The scattering law may be later provided to the THERMR module where the cross section can be determined and sorted according to incoming energy, outgoing energy, and scattering angle. 

A brief introduction to the scattering law is provided here: 

.. toctree::
   :maxdepth: 1

   inelastic/scatteringLaw


Inelastic scattering works in the **incoherent approximation**, which assumes that all inelastic scattering events in a material can be approximated as incoherent (meaning no periodic amplification/destruction of scattered neutron waves). This approximation is applied out of necessity, as accounting for coherent inelastic scattering events is a very difficult (and often unnecessary) step. Be aware, however, that for strong coherent scatterers in crystalline lattices, this approximation may not suffice. 


Since inelastic scattering is dependent on the creation and destruction of the scattering material's phonons, treatment of the phonon spectrum is crucial. LEAPR decomposes the phonon distribution into three parts: a solid-type spectrum, a translational term, and discrete oscillators. This decomposition and the treatment of these individual parts are described in the following sections:

.. toctree::
   :maxdepth: 4

   inelastic/phononDecomposition
   inelastic/continuous
   inelastic/translational
   inelastic/discrete

---------------------------------------
Coherent Elastic Scattering 
---------------------------------------

Elastic thermal neutron scattering is when a neutron scatters off of some target material without creating/destroying phonons, such that no neutron energy change occurs. The incoherent approximation is used with inelastic scattering, since accounting for inelastic coherence requires special treatment. With assuming that neutron energy *does not* change, however, coherent scattering calculations are quite feasible. 

Coherent elastic scattering calculations should be performed for crystalline materials comprised of strong coherent scatterers, such as Graphite, Beryllium, Beryllium Oxide, Aluminum, Lead, and Iron. The coherent elastic scattering treatment in LEAPR is intended for BCC, FCC, and Hexagonal lattices, and can treat the aforementioned materials.


.. toctree::
   :maxdepth: 1

   cohElastic/bragg
   cohElastic/equations


.. _incoherent_elastic:

---------------------------------------
Incoherent Elastic Scattering 
---------------------------------------

Elastic thermal neutron scattering is when a neutron scatters off of some target material without creating/destroying phonons, such that no neutron energy change occurs. **Incoherent** elastic thermal neutron scattering is when the scattered neutron waves do not constructively/destructively interfere. This is important for strong incoherent scatterers, particularly hydrogeneous solids such as solid methane, polyethylene, and zirconium hydride.

.. toctree::
   :maxdepth: 1

   incElastic/incElastic


.. _suggested_readings:

---------------------------------------
Further Reading
---------------------------------------

This guide is only intended to serve as a preliminary look into LEAPR's treatment of thermal neutron scattering. For a more rigorous treatments and further explanations, please consult the following texts:

- *Introduction to the Theory of Thermal Neutron Scattering* by G.L. Squires

- *Slow Neutron Scattering and Thermalization, with Reactor Applications* by D. E. Parks

- *Nuclear Reactor Theory* [Chapter 7] by G. I. Bell & S. Glasstone



.. .. toctree::
    :maxdepth: 4

..     suggestedReadings
    



.. Indices and tables
.. ==================

.. * :ref:`genindex`
.. * :ref:`modindex`
.. * :ref:`search`
