.. This is a comment. Note how any initial comments are moved by
   transforms to after the document title, subtitle, and docinfo.

.. demo.rst from: http://docutils.sourceforge.net/docs/user/rst/demo.txt

.. |EXAMPLE| image:: _images/temp.png
   :width: 1em

.. .. .. _theory:

***********************************************
Coherent Inelastic Approximations
***********************************************

Vineyard Approximation
========================

.. While preparing the scattering law (for inelastic thermal scattering processes), it is standard to use the incoherent approximation. As introduced in :ref:`incoherent_approximation`, the incoherent approximation neglects the distinct contribution of the pair distribution function, which neglects interference between different atoms. In reality, however, scattered from different molecules do interfere, which results when there is a correlation between the positions of nearby molecules. This kind of coherence is described by the "static structure factor" :math:`S(\kappa)`. This quantity can be used the **Vineyard Approximation**,

.. .. math::
  \frac{\partial^2\sigma}{\partial\Omega\partial\epsilon}=\frac{\partial^2\sigma_{coh}}{\partial\Omega\partial\epsilon}~S(\kappa)+\frac{\partial^2\sigma_{incoh}}{\partial\Omega\partial\epsilon}

.. As mentioned in :ref:`inelastic`, typical inelastic calculations assume that the nuclear spins are randomly oriented. For some materials (e.g., cold hydrogen or cold deuterium), there 




.. The incoherent approximation is used while preparing the scattering law for inelastic thermal scattering collisions. 

While preparing the scattering law (for inelastic thermal scattering processes), it is standard to use the incoherent approximation. As introduced in :ref:`incoherent_approximation`, the incoherent approximation neglects the distinct contribution of the pair distribution function, which neglects interference between different atoms. 

Intermolecular interference occurs when there is both a significant bound coherent scattering cross section (property of the atoms) as well as some correlation between the positions of nearby molecules (property of the lattice). If these requirements are met, coherent scattering may become non-negligible, at which point its effect can be accounted for by using the **Vineyard** approximation. 



.. In reality, however, scattered from different molecules do interfere, which results when there is a correlation between the positions of nearby molecules. This kind of coherence is described by the "static structure factor" :math:`S(\kappa)`. This quantity can be used the **Vineyard Approximation**,


.. , which is made while using the continuous, translational, and discrete oscillator methods, ignores coherent effects. There are some material, however, in which scattered neutron waves can interfere with each other in meaningful ways. This inter-molecular coherence occurs when there is both a significant bound coherent scattering cross section (property of the atoms) as well as some correlation between the positions of nearby molecules (property of the lattice). If these requirements are met, coherent scattering may become non-negligible, at which point its effect can be accounted for by using the **Vineyard** or **Skold** approximations. 

Here, the scattering law is separated into a coherent and an incoherent contribution, which are weighted using a *coherent fraction* :math:`c`. The incoherent contribution to the scattering law can be obtained using the phonon density of states (which is explained more further in [LINK TO LEAPR DOCUMENTATION HERE]), but the coherent contribution must be approximated.

.. math:: 
  S(\alpha,\beta)=\big(1-c\big)S_{inc}(\alpha,\beta)+c~S_{coh}(\alpha,\beta)


The Skold approximation approximates the coherent scattering law by using the *static structure factor* :math:`S(\kappa)` to modify the incoherent scattering law.

.. math:: 
  S_{coh}(\alpha,\beta)=S_{inc}\left(\frac{\alpha}{S(\kappa)},\beta\right)\times S(\kappa)

The static structure factor :math:`S(\kappa)` is a user-provided input that describes correlation in molecular positions, where :math:`\kappa` is wave number, defined as 

.. math:: 
  \kappa = \frac{\sqrt{2Mk_bT\alpha}}{\hbar}


where :math:`M` is the mass of the scatterer. Using these relations, the coherent-corrected scattering can be obtained by solving the above three equations for all :math:`\alpha,\beta` values.



