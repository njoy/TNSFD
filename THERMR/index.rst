.. cats documentation master file, created by
   sphinx-quickstart on Mon Jul 22 12:49:03 2019.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

The THERMR Module of NJOY
=====================================

The THERMR module generates pointwise neutron scattering cross sections in the thermal energy range and adds them to an existing PENDF file, which can then be further processed [group averaged, plotted, or reformatted] by other NJOY modules. 

Here, we provide an overview of THERMR, illustrate how to use it, and provide input instructions and examples. For new users, we recommend beginning with the overview and then looking through the explained examples. 

.. toctree::
   :maxdepth: 1

   overview/overview.rst





Coherent Elastic
--------------------

The energy grid for coherent elastic scattering is produced adaptively so as to represent the cross sections between the sharp Bragg edges to a specified tolerance using linear interpolation.

.. toctree::
   :maxdepth: 1

   coherentElastic/coherentElastic


Incoherent Elastic
--------------------

Incoherent cross sections are computed by integrating the incoherent distributions for consistency. 

.. toctree::
   :maxdepth: 1

   incoherentElastic/incoherentElastic


Inelastic
--------------------


The secondary energy grid for inelastic incoherent scattering when using :math:`E-E'-\mu` ordering is produced adaptively so as to represent all structure with linear interpolation. Discrete-angle representations are used to avoid the limitations of Legendre expansions.

An option to use :math:`E-\mu-E'` ordering is available. Dependences on :math:`\mu` and :math:`E'` are constructed adaptively.

.. toctree::
   :maxdepth: 1

   inelastic/inelastic 






