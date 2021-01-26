.. cats documentation master file, created by
   sphinx-quickstart on Mon Jul 22 12:49:03 2019.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

The THERMR Module of NJOY
=========================

The THERMR module generates pointwise neutron scattering cross sections in the thermal energy range and adds them to an existing PENDF file, which can then be further processed [group averaged, plotted, or reformatted] by other NJOY modules. 

Here, we provide an overview of THERMR, illustrate how to use it, and provide input instructions and examples. For new users, we recommend beginning with the overview and then looking through the explained examples. 

You can find out more at :ref:`overview of THERMR<overview>`.

.. toctree::
   :maxdepth: 1
   :caption: Contents:
   :hidden:

   overview.rst
   coherentElastic
   incoherentElastic
   inelastic 
   usersManual
   examples/index


Coherent Elastic
--------------------

The energy grid for coherent elastic scattering is produced adaptively so as to represent the cross sections between the sharp Bragg edges to a specified tolerance using linear interpolation. 

More information on the treatment of coherent elastic scattering treatment in THERMR is available at :ref:`coherent elastic scattering<coherentElastic>`.

Incoherent Elastic
--------------------

.. Incoherent cross sections are computed by integrating the incoherent distributions for consistency. 

Incoherent elastic scattering is a scattering event in which the neutron neither changes energy nor experiences coherent scattering effects (e.g. periodic constructive amplification or destructive cancellation). THERMR calculates the average cross section value for a given energy (averaged across angles), while also generating the equi-probable cosines for each energy. 


For more information on the treatment of incoherent elastic scattering data, visit :ref:`incoherent elastic scattering<incoherentElastic>`.

Inelastic
--------------------


The secondary energy grid for inelastic incoherent scattering when using :math:`E-E'-\mu` ordering is produced adaptively so as to represent all structure with linear interpolation. Discrete-angle representations are used to avoid the limitations of Legendre expansions.

An option to use :math:`E-\mu-E'` ordering is available. Dependences on :math:`\mu` and :math:`E'` are constructed adaptively, and more information is available at :ref:`inelastic scattering data<inelastic>`.


User's Manual
=======================

After familiarization with the data used to describe the various types of thermal neutron scattering, exploring the options available in THERMR can prove helpful. In the :ref:`user's manual<usersManual>` we describe and explain the different options available to you with THERMR.



Example Inputs
=======================

To briefly illustrate the abilities of THERMR, example THERMR inputs are provided in the :ref:`examples<examplesMain>` directory. 










