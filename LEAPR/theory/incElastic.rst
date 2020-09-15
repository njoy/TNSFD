
..
  COMMENT: .. contents:: Table of Contents


In the phonon expansion method for continuous, solid-type data, we saw that the zero-phonon term to :math:`S_s(\alpha,\beta)`,

.. math::
  \mathrm{e}^{-\alpha\lambda_s}~\delta(\beta)

was left out, to be handled separately. 


Translational Component Included 
----------------------------------

If a translational term is considered, then the translational and continuous scattering law contributions are combined as follows:

.. math::
  S(\alpha,\beta) = S_t(\alpha,\beta)~\mathrm{e}^{-\alpha\lambda_s} + \int_{-\infty}^\infty S_t(\alpha,\beta')~S_s(\alpha,\beta-\beta')~d\beta'

Note that while doing this convolution, the values of the translational piece :math:`S_t(\alpha,\beta')` and the solid-type piece :math:`S_s(\alpha,\beta-\beta')` are precomputed and interpolated on.



No Translational Component Included 
---------------------------------------

If the user does not request that a translational component be considered in while preparing the scattering data, then the zero-phonon term must be added separately. This is handled as "incoherent elastic scattering",

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

where :math:`A` is the ratio of the scatterer mass to the neutron mass, and :math:`\lambda` can be readily computed from the phonon density of states, as was seen in :ref:`continuous_solid_type`.


LEAPR writes the bound scattering cross section :math:`\sigma_b` and the Debye-Waller factor :math:`W` as a function of temperature into a section of ENDF-6 output with MF=7 and MT=2.


.. This is done by adding in triangular peaks with the proper areas and with their apexes at the :math:`\beta` value closest to the :math:`\beta_k

