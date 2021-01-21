
.. _inelastic:

**********************
Inelastic
**********************

..
  COMMENT: .. contents:: Table of Contents

Inelastic thermal neutron scattering is often described in terms of the "scattering law" :math:`S(\alpha,\beta)` which is a function of unitless momentum exchange :math:`\alpha` and unitless energy exchange :math:`\beta`. In the incoherent approximation, we find that 

.. math::
  \sigma(E,E',\mu) = \frac{\sigma_b}{2k_bT}~\sqrt{\frac{E'}{E}}~\mathrm{e}^{-\beta/2}~S_{sym}(\alpha,\beta)


where :math:`\sigma_b` is the bound scattering cross section, :math:`k_bT` is the temperature in eV, :math:`E,E'` are the incoming, outgoing neutron energies, and :math:`S_{sym}(\alpha,\beta)` is the symmetric form of the thermal neutron scattering law. For a more detailed explanation of this equation and how the scattering law is prepared for various materials, please consult the LEAPR documentation. 



The scattering law is often prepared by the LEAPR module and written to MF=7/MT=4 format as a table of :math:`S` verses :math:`\alpha` and :math:`\beta` values. Values of :math:`S` for :math:`\alpha,\beta` not on the written grid can be obtained via interpolation. The scattering law is normally symmetric in :math:`\beta`, but for materials like orthohydrogen and parahydrogen (which are of interest as cold moderators for neutron scattering facilities), this no longer holds and the symmetric behavior of the scattering law is broken. In these cases, the scattering law must be tabulated for both positive and negative :math:`\beta`. 




If the :math:`\alpha` or :math:`\beta` required is outside the range of the table provided to LEAPR in File 7, then the differential scattering cross section can be computed using the short-collision time (SCT) approximation,

.. math:: 
  \sigma^{SCT}(E,E',\mu)=\frac{\sigma_b}{2k_bT}\frac{\sqrt{E'/E}}{\sqrt{4\pi~\alpha~T_{eff}/T}}~\mathrm{exp}\left[-\frac{(\alpha-|\beta|)^2}{4\alpha}\frac{T}{T_{eff}}-\frac{\beta+|\beta|}{2}\right]

where the effective temperature :math:`T_{eff}` is provided in the data file. 

THERMR expects the requested temperatures :math:`T` to be one of the temperatures included on the input ENDF/B thermal scattering file (or within a few degrees of that value). Scattering data for intermediate temperatures should always be obtained by interpolating the cross section and not by interpolating the scattering law :math:`S(\alpha,\beta)`.



