
**********************
Overview
**********************

..
  COMMENT: .. contents:: Table of Contents


If a neutron has sufficiently high energy prior to a scattering event, then we may neglect the molecular bonds of the target atom, and thus assume that the target atom was free and unbound. Thermal neutrons are defined as those for which this assumption is no longer valid, and have energy of a few eV or less.  

.. Due to the vital role that these thermal neutrons play in many reactor systems, the ability to accurately simulate a reactor often relies on the thermal scattering data provided to the simulation. 

**The role of the LEAPR module is to prepare thermal neutron scattering data for use in reactor system simulations.**


.. , which play a vital role in many nuclear reactor systems. 

.. In the incoherent approximation, the thermal scattering cross section is defined as 

.. .. math::
    \sigma(E\rightarrow E',\mu) = \frac{\sigma_b}{k_bT}\sqrt{\frac{E'}{E}}~S(\alpha,\beta)
 
.. where :math:`S(\alpha,\beta)` is the thermal scattering law. The purpose of LEAPR is to prepare the scattering law (along with Bragg edges, Debye-Waller factors, etc.) for further use by supplementary codes like the THERMR module. 


Thermal neutron scattering can be categorized as either elastic or inelastic, both of which can have coherent and incoherent contributions. Modern thermal scattering data processing codes typically combine coherent inelastic with incoherent inelastic in what is called the incoherent approximation.


With this approximation, LEAPR is prepared to handle the following thermal scattering types:

.. Typically, thermal scattering is divided into the following categories:



:Incoherent elastic: This is important for hydrogeneous solids like solid methane, polyethylene, and zirconium hydride. For this, LEAPR calculates the Debye-Waller coefficients for desired temperatures, which can be used to later calculate the incoherent elastic cross sections.


:Coherent elastic: This is important for crystalline solids such as graphite and Beryllium. LEAPR prepares the locations and weights of the coherent elastic Bragg edges. 


:Inelastic scattering: This is important for all materials. To describe this data, LEAPR prepares the scattering law :math:`S(\alpha,\beta)`. LEAPR works in the incoherent approximation, which allows the scattering law to be calculated using the phonon density of states (also known as the phonon distribution). 

  While calculating the scattering law from the phonon distribution, LEAPR employs the "phonon decomposition approach" and separates the phonon distribution into three components: a solid-type continuous contribution, a discrete-oscillator contribution, and a translational contribution. These three components of the phonon distribution will be further described in the theory section.

  How NJOY handles these three types of scattering will be explained in subsequent sections.



 
.. 1. **Incoherent elastic**
   This is important for hydrogeneous solids like solid methane, polyethylene, and zirconium hydride. For this, LEAPR calculates the Debye-Waller coefficients for desired temperatures, which can be used to later calculate the incoherent elastic cross sections.



.. 2. **Coherent elastic**
   This is important for crystalline solids such as graphite and Beryllium. LEAPR prepares the locations and weights of the coherent elastic Bragg edges. 




.. 3. **Inelastic scattering** 
   This is important for all materials. To describe this data, LEAPR prepares the scattering law :math:`S(\alpha,\beta)`. As mentioned above, LEAPR works in the incoherent approximation, which allows the scattering law to be calculated using the phonon density of states (also known as the phonon distribution). 
   While calculating the scattering law from the phonon distribution, LEAPR employs the "phonon decomposition approach" and separates the phonon distribution into three components: a solid-type continuous contribution, a discrete-oscillator contribution, and a translational contribution. These three components of the phonon distribution will be further described in the theory section.

.. How NJOY handles these three types of scattering will be explained in subsequent sections.


