
Representation of Incoherent Elastic through Debye-Waller Factors
--------------------------------------------------------------------

..
  COMMENT: .. contents:: Table of Contents

In :ref:`continuous_solid_type`, we found that the phonon expansion for solid-type spectra resulted in the following sum:

.. math::
  S_s(\alpha,\beta) \approx \mathrm{e}^{-\alpha\lambda_s}~\sum_{n=1}^N\frac{1}{n!}\Big[\alpha\lambda_s\Big]^n\mathcal{T}_n(\beta)

where :math:`n` corresponds to the number of phonons created/destroyed in a collision. This summation used intentionally left out the :math:`n=0` term (which, since no phonons are created/destroyed, corresponds to elastic scattering). The zero-phonon term is intead considered here, so that if translational motion is desired, it can be properly treated. 


**No Translational Component Included**

If the user does not request that a translational component be considered in while preparing the scattering data, then the zero-phonon term may simply be added without additional steps. 


.. math::
 S_{inc.el}(\alpha,\beta)=\mathrm{e}^{-\alpha\lambda}~\delta(\beta).

The corresponding differential scattering cross section is 

.. math::
  \sigma(E,\mu)=\frac{\sigma_b}{2}~\mathrm{e}^{-2WE(1-\mu)}

and the integrated cross section is 

.. math::
  \sigma(E) = \frac{\sigma_b}{2}~\frac{1-\mathrm{e}^{-4WE}}{2WE}.

Where the Debye-Waller factor :math:`W` is computed using the Debye-Waller coefficient :math:`\lambda`,

.. math::
  W=\frac{\lambda}{Ak_bT},

where :math:`A` is the ratio of the scatterer mass to the neutron mass and :math:`\lambda` can be readily computed from the phonon density of states, as was seen in :ref:`continuous_solid_type`.


LEAPR writes the bound scattering cross section :math:`\sigma_b` and the Debye-Waller factor :math:`W` as a function of temperature into a section of ENDF-6 output with MF=7 and MT=2.


.. This is done by adding in triangular peaks with the proper areas and with their apexes at the :math:`\beta` value closest to the :math:`\beta_k







**Translational Component Included**

If a translational term is considered, then the translational and continuous scattering law contributions are combined as follows:

.. math::
  S(\alpha,\beta) = S_t(\alpha,\beta)~\mathrm{e}^{-\alpha\lambda_s} + \int_{-\infty}^\infty S_t(\alpha,\beta')~S_s(\alpha,\beta-\beta')~d\beta'

Note that while doing this convolution, the values of the translational piece :math:`S_t(\alpha,\beta')` and the solid-type piece :math:`S_s(\alpha,\beta-\beta')` are precomputed and interpolated on.




