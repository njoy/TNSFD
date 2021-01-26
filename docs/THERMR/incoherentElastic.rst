
.. _incoherentElastic:

**********************
Incoherent Elastic
**********************

..
  COMMENT: .. contents:: Table of Contents

.. In some material (particularly hydrogenous solids), there is an elastic component of thermal neutron scattering that arises from the zero-phonon term of the phonon expansion in the incoherent approximation. 

In some materials (particularly hydrogeneous solids), elastic thermal neutron scattering is almost entirely incoherent (e.g. no periodic constructive amplification or destructive cancellation of neutron waves). This scattering, which is denoted as incoherent elastic scattering, can be treated in the incoherent approximation that is vital to LEAPR's preparation of the scattering law. In this approximation, LEAPR assumes that the coherent term of inelastic scattering is negligible, which allows for the so-called "phonon expansion" sum to be performed. For more information on the phonon expansion, please consult the LEAPR documentation. 

The zeroth term of the phonon expansion (indicating to the creation/destruction of zero phonons) corresponds to the incoherent elastic scattering term. This is a simple treatment that allows us to write the differential incoherent elastic scattering cross section as

.. math::
  \sigma^{inc.el}(E,\mu)=\frac{\sigma_b}{2}~\mathrm{e}^{-2WE(1-\mu)}

where :math:`\sigma_b` is the bound scattering cross section of the material, and :math:`W` is the Debye-Waller coefficient. Here, :math:`W` can be determined using the Debye-Waller factor :math:`\lambda` (obtained by LEAPR from the phonon distribution), the ratio of the scatterer mass to neutron mass :math:`A`, and the temperature in eV :math:`k_bT`,

.. math::
  W=\frac{\lambda}{Ak_bT}.

and in practice, these Debye-Waller values are obtianed from the MF=6/MT=2 section of the ENDF-6 format evaluation.

For every energy point on the neutron energy grid, the average cross section (averaged across scattering cosines) is calculated,

.. math::
  \sigma^{inc.el.}(E)=\frac{\sigma_b}{2}~\left[\frac{1-\mathrm{e}^{-4WE}}{2WE}\right]

along with the equi-probable cosines of that energy,

.. math::
  \begin{align}
  \bar{\mu_i}=\frac{N_{bin}}{2WE}\Big[&\mathrm{e}^{-2WE(1-\mu_{i~~~~})}~(2WE\mu_{i~~~~}-1) \\
   &\mathrm{e}^{-2WE(1-\mu_{i-1})}~(2WE\mu_{i-1}-1)\Big]~\left[1-\mathrm{e}^{-4WE}\right]^{-1}
  \end{align}


where 

.. math:: 
  \mu_i = 1+\frac{1}{2WE}~\ln\left[\frac{1-\mathrm{e}^{-4WE}}{N_{bin}}+\mathrm{e}^{-2WE(1-\mu_{i-1})}\right]. 

In the above equations, :math:`N_{bin}` is the number of equi-probable bins and :math:`\mu_0=-1`. 





