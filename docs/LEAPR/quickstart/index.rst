.. _quickstart:

=====================================
Quickstart
=====================================

It is recommended that new users of the NJOY LEAPR module review example inputs to ensure proper use of the code. Here, we walk through a set of different inputs to illustrate NJOY capability. We recommend beginning with the single-temperature Fe-56 example first, as it outlines the basics of calling LEAPR before performing more advanced calculations that involve multiple temperatures or molecular coherence.


.. ---------------------------------
.. Single-Temperature Fe-56
.. ---------------------------------

.. rubric:: Single-Temperature Fe-56

This single temperature Fe-56 example...

- Processes thermal scattering data at a single material temperature
- Considers only a primary scatterer
- Uses only the solid-type distribution to describe inelastic scattering 

This example uses very coarse :math:`\alpha` and :math:`\beta` grids and an inaccurate solid-type spectrum, so it is not recommended for realistic calculations and is only for instructional use. 


.. toctree::
   :maxdepth: 1

   fe 



.. rubric:: Simple H in H2O

This simple H in H2O example...

- Processes thermal scattering data at a single material temperature
- Considers both a primary and a secondary scatterer 
- Uses all three components to inelastic scattering (solid type, translational, and discrete oscillators)

The simple H in H2O example uses very coarse :math:`\alpha` and :math:`\beta` grids and an inaccurate solid-type spectrum, so it is not recommended for realistic calculations and is only for instructional use. 


.. toctree::
   :maxdepth: 0

   h2o_simple


.. ------------------------------------------------
.. Advanced H in H2O 
.. ------------------------------------------------


.. rubric:: Advanced H in H2O 


This H in H2O example...

- Processes thermal scattering data at multiple temperatures
- Uses different phonon distribution specifications for each temperature
- Considers both a primary and a secondary scatterer 
- Uses all three components to inelastic scattering (solid type, translational, and discrete oscillators)

The main purpose of this example is to illustrate how to process thermal scattering data for different temperatures, where each temperature is characterized using a different phonon distribution.

.. toctree::
   :maxdepth: 1

   h2o_multipleTemps
