
Translational/Diffusive Behaviour
-----------------------------------

The neutron scattering from many liquids (e.g., water and liquid methane) can be represented using a solid-type scattering law :math:`S_s(\alpha,\beta)` and convolving it with a translational scattering law :math:`S_t(\alpha,\beta)`. There are two options for the translational term: the effective width model, and the free gas model. 

**Effective Width Model**

Egelstaff and Schofield have proposed an especially simple model for diffusion called the "effective width model", which has analytical forms for both :math:`S_t(\alpha,\beta)` and the associated frequency distribution function :math:`\rho_t(\beta)`.

.. math:: 
  S_t(\alpha,\beta)=\frac{2c\omega_t\alpha}{\pi}~\mathrm{exp}\Big[2c^2\omega_t\alpha-\beta/2\Big]~\sqrt{\frac{c^2+0.25}{\beta^2+4c^2\omega_t^2\alpha^2}}~K_1\Big[\sqrt{c^2+0.25}\sqrt{\beta^2+4c^2\omega_t^2\alpha^2}\Big]

.. math::
  \rho_t(\beta)=\frac{4c\omega_t}{\pi\beta}\sqrt{c^2+0.25}~\sinh(\beta/2)~K_1\left[\beta\sqrt{c^2+0.25}\right]

where :math:`K_1(x)` is a modified Bessel function of the second kind, :math:`\omega_t` is the translational weight, and :math:`c` is the diffusion constant.

**Free Gas Model**

Alternatively, the translational term can be represented using a free gas model. While a free gas model is obviously most applicable for cloud of non-interacting gas atoms, it has been used to represent the translation component for liquid moderators. 

.. math:: 
  S_t(\alpha,\beta)=\frac{1}{\sqrt{4\pi\omega_t\alpha}}~\mathrm{exp}\left[\frac{-(\omega_t\alpha+\beta)^2}{4\omega_t\alpha}\right]

..  S_t(\alpha,-\beta)=\frac{1}{\sqrt{4\pi\omega_t\alpha}}~\mathrm{exp}\left[-\frac{(\omega_t\alpha-\beta)^2}{4\omega_t\alpha}\right]

..  S_t(\alpha,\beta)=\mathrm{e}^{-\beta}\frac{1}{\sqrt{4\pi\omega_t\alpha}}~\mathrm{e}^{\left[-\frac{(\omega_t\alpha-\beta)^2}{4\omega_t\alpha}\right]}

..  S_t(\alpha,\beta)=\frac{1}{\sqrt{4\pi\omega_t\alpha}}~\mathrm{e}^{\frac{-(\omega_t\alpha-\beta)^2}{4\omega_t\alpha}-\frac{\beta4\omega_t\alpha}{4\omega_t\alpha}}

..  S_t(\alpha,\beta)=\frac{1}{\sqrt{4\pi\omega_t\alpha}}~\mathrm{e}^{\frac{-\omega_t^2\alpha^2-\beta^2+2\omega_t\alpha\beta}{4\omega_t\alpha}-\frac{\beta4\omega_t\alpha}{4\omega_t\alpha}}

..  S_t(\alpha,\beta)=\frac{1}{\sqrt{4\pi\omega_t\alpha}}~\mathrm{e}^{\frac{-\omega_t^2\alpha^2-\beta^2-2\omega_t\alpha\beta}{4\omega_t\alpha}}

..  S_t(\alpha,\beta)=\frac{1}{\sqrt{4\pi\omega_t\alpha}}~\mathrm{e}^{\frac{-(\omega_t\alpha+\beta)^2}{4\omega_t\alpha}}

.. **Effective Temperature**

.. If a translational component is considered, the effective temperature is updated as follows:

.. .. math::
  \overline{T}=\frac{\omega_t T+\omega_s\overline{T}_s}{\omega_t+\omega_s}


.. The LEAPR module is used to prepare the thermal scattering law :math:`S(\alpha,\beta)`, which describes thermal scattering from bound moderators. 

.. LEAPR uses the incoherent approximation for preparing the thermal scattering data. 


