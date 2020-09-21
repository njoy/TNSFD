
**********************
Overview
**********************

..
  COMMENT: .. contents:: Table of Contents


In the incoherent approximation, the thermal scattering cross section is defined as 

.. math::
    \sigma(E\rightarrow E',\mu) = \frac{\sigma_b}{k_bT}\sqrt{\frac{E'}{E}}~S(\alpha,\beta)
 
where :math:`S(\alpha,\beta)` is the thermal scattering law. The purpose of LEAPR is to prepare the scattering law (along with Bragg edges, Debye-Waller factors, etc.) for further use by supplementary codes like the THERMR module. 


Thermal neutron scattering can be categorized as either elastic or inelastic, both of which can have coherent and incoherent contributions. Modern thermal scattering data processing typically combines coherent inelastic with incoherent inelastic in what is called the incoherent approximation.


With this approximation, NJOY is prepared to handle the following thermal scattering types:

.. Typically, thermal scattering is divided into the following categories:

1. **Incoherent elastic**
   This is important for hydrogeneous solids like solid methane, polyethylene, and zirconium hydride. 
2. **Coherent elastic**
   This is important for crystalline solids such as graphite and Beryllium. LEAPR prepares the locations of the Bragg edges and their weights. 
3. **Inelastic scattering** (in the incoherent approximation)
   This is important for all materials. To describe this data, LEAPR needs to prepare the scattering law :math:`S(\alpha,\beta)`, and does so with the phonon density of states. The phonon distribution can be decomposed into three components: a solid-type continuous contribution, a discrete-oscillator contribution, and a translational contribution.




These three components of the phonon distribution will be further described in the theory section.

.. How NJOY handles these three types of scattering will be explained in subsequent sections.


