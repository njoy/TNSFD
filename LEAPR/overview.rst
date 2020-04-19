
**********************
NJOY Introduction 
**********************

..
  COMMENT: .. contents:: Table of Contents

Overview
=====================

In the incoherent approximation, the thermal scattering cross section is defined as 

.. math::
    \sigma(E\rightarrow E',\mu) = \frac{\sigma_b}{k_bT}\sqrt{\frac{E'}{E}}~S(\alpha,\beta)
 
where :math:`S(\alpha,\beta)` is the thermal scattering law. The purpose of LEAPR is to prepare the scattering law (along with Bragg edges, Debye-Waller factors, etc.) for further use by supplementary codes like the THERMR module. 


LEAPR is equipped to prepare thermal scattering data for

Typically, thermal scattering is divided into the following categories:

1. **Incoherent elastic**
   This is important for hydrogeneous solids like solid methane, polyethylene, and zirconium hydride. 
2. **Coherent elastic**
   This is important for crystalline solids such as graphite and Beryllium. LEAPR prepares the locations of the Bragg edges and their weights. 
3. **Inelastic scattering** (in the incoherent approximation)
   This is important for all materials. To describe this data, LEAPR needs to prepare the scattering law :math:`S(\alpha,\beta)`, and does so with the phonon density of states. The phonon distribution can be decomposed into three components: a solid-type continuous contribution, a discrete-oscillator contribution, and a translational contribution.





.. The LEAPR module is used to prepare the thermal scattering law :math:`S(\alpha,\beta)`, which describes thermal scattering from bound moderators. 

.. LEAPR uses the incoherent approximation for preparing the thermal scattering data. 




