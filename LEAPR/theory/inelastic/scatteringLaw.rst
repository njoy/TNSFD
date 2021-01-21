.. _scatteringLawInfo:

Scattering Law
==================


The thermal scattering cross section is defined as 

 .. math::
    \sigma(E\rightarrow E',\mu) = \frac{\sigma_b}{k_bT}\sqrt{\frac{E'}{E}}~S_{n.sym}(\alpha,\beta)
 
where :math:`S_{n.sym}(\alpha,\beta)` is the non-symmetric form of the thermal scattering law, :math:`\sigma_b` is the bound scattering cross section, and :math:`k_bT` is the temperature in eV. 

Here, :math:`\alpha` is unitless momentum exchange and :math:`\beta` is unitless energy exchange, as seen below:

.. math::
  \alpha = \frac{E'+E-2\mu\sqrt{E'E}}{Ak_bT}\\

.. math::
  \beta= \frac{E'-E}{k_bT}

where initial and final neutron energies are :math:`E` and :math:`E'` respectively, :math:`A` is the ratio of the scatterer mass to the neutron mass, and :math:`\mu` is the cosine of the scattering angle in the laboratory. 
Note that :math:`\beta` is positive for neutron energy gain and negative for neutron energy loss.


The purpose of LEAPR is to prepare the scattering law (along with Bragg edges, Debye-Waller factors, etc.) for further use by supplementary codes like the THERMR module.


.. _symmetricNonsymmetric:

Symmetric vs. Non-Symmetric
------------------------------

In the definition of the inelastic thermal neutron scattering cross section above, we made use of the non-symmetric scattering law :math:`S_{n.sym}(\alpha,\beta)`. For systems in thermal equilibrium, there is a relationship between upscatter and downscatter called "detail balance" that is a consequence of microscopic reversibility. It requies that 

.. math::
  S_{n.sym}(\alpha,\beta)=\exp^{-\beta}~S_{n.sym}(\alpha,-\beta). 

If we define a function :math:`S_{sym}(\alpha,\beta)` to be 

.. math::
  S_{sym}(\alpha,\beta) = \exp^{\beta/2}~S_{n.sym}(\alpha,\beta)

then the detail balance requirement states that 

.. math::
  S_{sym}(\alpha,\beta) = S_{sym}(\alpha,-\beta)

which indicates that :math:`S_{sym}(\alpha,\beta)` is a symmetric function in :math:`\beta`. Thus, :math:`S_{sym}(\alpha,\beta)` is known as the symmetric scattering law. 

.. note:: 
  The symmetry :math:`S_{sym}(\alpha,\beta)` is not present for liquid hydrogen or liquid deuterium. 


LEAPR performs all its calculations on :math:`S_{n.sym}(\alpha,-\beta)` because its contents have less extreme values than :math:`S_{sym}(\alpha,\beta)` or :math:`S_{n.sym}(\alpha,\beta)`. Typically, however, the scattering law is converted to :math:`S_{sym}(\alpha,\beta)` prior to being written to the output tape. 








