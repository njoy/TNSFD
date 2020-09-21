.. _quickstart:

=====================================
Quickstart
=====================================

It is recommended that new users of the NJOY LEAPR module review example inputs to ensure proper use of the code. Here, we walk through a set of different inputs to illustrate NJOY capability. We recommend beginning with the simple H in H2O example first, as it outlines the basics of calling LEAPR before performing more advanced calculations that involve multiple temperatures or molecular coherence.


---------------------------------
Simple H in H2O 
---------------------------------

This simple H in H2O example...
- Processes thermal scattering data at a single material temperature
- Considers both a primary and a secondary scatterer 
- Uses all three components to inelastic scattering (solid type, translational, and discrete oscillators)

The simple H in H2O example uses very coarse :math:`\alpha` and :math:`\beta` grids and an inaccurate solid-type spectrum, so it is not recommended for realistic calculations and is only for instructional use. 


.. toctree::
   :maxdepth: 1

   h2o_simple


------------------------------------
H in H2O for Multiple Temperatures
------------------------------------

This H in H2O example...
- Processes thermal scattering data at multiple temperatures
- Uses different phonon distribution specifications for each temperature
- Considers both a primary and a secondary scatterer 
- Uses all three components to inelastic scattering (solid type, translational, and discrete oscillators)

The main purpose of this example is to illustrate how to process thermal scattering data for different temperatures, where each temperature is characterized using a different phonon distribution.

.. toctree::
   :maxdepth: 1

   h2o_multipleTemps
