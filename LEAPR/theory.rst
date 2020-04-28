
**********************
Theory
**********************

..
  COMMENT: .. contents:: Table of Contents


Inelastic Scattering
======================

Phonon Decomposition
---------------------


To describe inelastic thermal neutron scattering, the scattering law :math:`S(\alpha,\beta)` must be obtained, which is performed using a phonon distribution. LEAPR performs a phonon decomposition, which means that a phonon distribution could consist of the following three contributions:

1. Continuous, solid-type spectrum
2. Translational, diffusive behavior
3. Discrete (Einstein) oscillators

The continuous spectrum (which requires a phonon distribution) is always required. The other two components are optional, and can be used to augment the existing phonon distribution to add very sharp peaks or fluid-like behaviour. 

.. math:: 
  \rho(\beta) = \rho_{solid}(\beta) + \underbrace{\rho_{trans.}(\beta)}_{\text{optional}} + \underbrace{\sum_{n=1}^{N_{osc}}\omega_n\delta(\beta_n) }_{\text{optional}}

The solid-type spectrum is assumed to vary as :math:`\beta^2` as :math:`\beta` goes to zero, and it must integrate to :math:`\omega_s`, which is the weight for the solid type law (this is a user provided value).

The translational spectrum integrates to the translational weight :math:`\omega_t` (user provided) and can be either a free gas law or a diffusion type spectrum.

The sum of all weights must add to unity:

.. math::
  \omega_s + \omega_t + \sum_{n=1}^{N_{osc}}\omega_n = 1


Using the phonon decomposition method, the final scattering law can be calculated by recursively convolving individual scattering laws. 


.. math:: 
  S(\alpha,\beta) = S^{(K)}(\alpha,\beta)

where

.. math::
  S^{(J)}(\alpha,\beta) = \int_{-\infty}^\infty S^{(J)}(\alpha,\beta')~S^{(J-1)}(\alpha,\beta-\beta')~d\beta'. 


**Debye-Waller Coefficient**
 
The Debye-Waller coefficient is a temperature-dependent quantity that is related to the average displacement of an atom from its equilibrium position. The full Debye-Waller coefficient :math:`\lambda` is the combination of the solid-type value :math:`\lambda_s` and and discrete oscillator values :math:`\lambda_i`,

.. math::
  \lambda = \lambda_s + \sum_{i=1}^{N_{osc}}\lambda_i.

Note that the translational component is not represented in the Debye-Waller coefficient.

**Effective Temperature**

The effective temperature for all modes is defined as 

.. math::
  \overline{T} = \omega_t~T + \omega_s~\overline{T}_s+\sum_{i=1}^{N_{osc}}\omega_i\frac{\beta_i}{2}~\coth(\beta_i/2)~T

where :math:`\omega_t,\omega_s,` and :math:`\omega_i` are the fractional weights for the translational piece, the solid-type piece, and each oscillator.


-------------------------------------------------

**Example**

As an example, consider a phonon distribution that is comprised of a continuous component :math:`[\rho_s(\beta)]` and two discrete oscillators :math:`[\rho_{d1}(\beta)` and :math:`\rho_{d2}(\beta)]`. These three phonon contributions generate corresponding scattering law components :math:`S_s(\alpha,\beta),S_{d1}(\alpha,\beta),S_{d2}(\alpha,\beta)`.

The zeroth term consists solely of the continuous, solid-type contribution :math:`S_s(\alpha,\beta)`

.. math::
  S^{(0)}(\alpha,\beta) = S_s(\alpha,\beta) 

and we convolve the second scattering law :math:`S_{d1}(\alpha,\beta)` with the zeroth term,

.. math::
  \begin{align}
  S^{(1)}(\alpha,\beta) &= \int_{-\infty}^\infty S_{d1}(\alpha,\beta')~S^{(0)}(\alpha,\beta-\beta')~d\beta'\\
                        &= \int_{-\infty}^\infty S_{d1}(\alpha,\beta')~S_s(\alpha,\beta-\beta')~d\beta'\\
  \end{align}

and the last scattering law :math:`S_{d2}(\alpha,\beta)` is convolved with :math:`S^{(1)}(\alpha,\beta)`,

.. math::
  \begin{align}
  S^{(2)}(\alpha,\beta) &= \int_{-\infty}^\infty S_{d2}(\alpha,\beta')~S^{(1)}(\alpha,\beta-\beta')~d\beta'\\
  \end{align}


and :math:`S^{(2)}(\alpha,\beta)` is the final scattering law that combines these three components.


-------------------------------------------------





.. _continuous_solid_type:

Continuous, Solid-type Spectrum
-------------------------------

For a solid-type spectrum, the scattering law is defined as 

 .. math::
     S_s(\alpha,\beta) = \frac{1}{2\pi}\int_{-\infty}^\infty\mathrm{e}^{i\beta t}~\mathrm{e}^{\gamma(t)-\gamma(0)}~dt

.. math::
    \gamma(t)=\alpha\int_{-\infty}^\infty P(\beta) ~\mathrm{e}^{-i\beta t}~\mathrm{e}^{-\beta/2}~d\beta

where 

.. math::
  P(\beta) = \frac{\rho(\beta)}{2\beta\sinh(\beta/2)}

and the phonon distribution :math:`\rho(\beta)` is and even funcion and is normalized to the solid-type distribution weight :math:`\omega_s`, 

.. math::
  \int_0^\infty\rho(\beta)~d\beta=\omega_s.

The phonon distribution can be input without normalization - it will be normalized automatically by LEAPR.

Recall that while :math:`\beta` is defined as unitless energy change :math:`(E'-E)/k_bT`, the input phonon distribution must be provided energy exchange :math:`E'-E` in units of eV.

.. Recall that :math:`\beta` is unitless neutron energy exchange

.. .. math::
  \beta=\frac{E'-E}{k_bT}

.. Although the phonon distribution :math:`\rho(\beta)` is shown as a function of :math:`\beta`, it is given to LEAPR as a function of energy exchange :math:`|E'-E|` (in eV).

.. Although the phonon distribution is used here as a function of :math:`\beta`, it will be provided as a function of energy,

The Debye-Waller coefficient is defined as 

.. math::
  \lambda_s = \int_{-\infty}^\infty P(\beta)~\mathrm{e}^{-\beta/2}~d\beta

which simplifies the scattering law :math:`S_s(\alpha,\beta)` to be 

 .. math::
     S_s(\alpha,\beta) = \frac{1}{2\pi}\mathbf{e}^{-\alpha\lambda_s}\int_{-\infty}^\infty\mathrm{e}^{i\beta t}~\mathrm{e}^{\gamma(t)}~dt

**Phonon Expansion**

The exponential of :math:`\gamma(t)` is a complex and highly oscillatory. 

.. math::
  \mathrm{e}^{\gamma(t)}=\mathrm{exp}\left[ \alpha\int_{-\infty}^\infty P(\beta)~\mathrm{e}^{-i\beta t}~\mathrm{e}^{-\beta/2}~d\beta  \right]\\

To ease the burden of calculating the scattering law, LEAPR uses the phonon expanion method, which involves expanding the :math:`\gamma(t)` exponential as a Taylor series, 

.. math::
   \mathrm{e}^{\gamma(t)} =\sum_{n=0}^\infty\frac{1}{n!}\left[ \alpha\int_{-\infty}^\infty P(\beta)~\mathrm{e}^{-i\beta t}~\mathrm{e}^{-\beta/2}~d\beta  \right]^n

which, when used in the solid-type scattering law definition, results in

.. .. math::
..      S(\alpha,\beta) = \frac{1}{2\pi}\mathbf{e}^{-\alpha\lambda_s} \sum_{n=0}^\infty\int_{-\infty}^\infty\mathrm{e}^{i\beta t}~\frac{1}{n!}\left[ \alpha\int_{-\infty}^\infty \frac{\rho(\beta)}{2\beta\sinh(\beta/2)}~\mathrm{e}^{-i\beta t}~\mathrm{e}^{-\beta/2}~d\beta  \right]^n~dt.

.. The order of summation and integral can swapped, and 

.. math::
  \begin{align}
     S_s(\alpha,\beta) =~&\mathbf{e}^{-\alpha\lambda_s} \sum_{n=0}^\infty \frac{1}{n!}\alpha^n \\
     \times~&\frac{1}{2\pi} \int_{-\infty}^\infty\mathrm{e}^{i\beta t}~\left[ \int_{-\infty}^\infty P(\beta)~\mathrm{e}^{-i\beta t}~\mathrm{e}^{-\beta/2}~d\beta  \right]^n~dt
  \end{align}

(note that the order of summation and integral have been swapped). Now, the second line of the above equation is redefined as :math:`\lambda_s^n\mathcal{T}_n(\beta)`. This allows for the solid-type scattering law to be redefined as 

.. math::
  S_s(\alpha,\beta) = \mathrm{e}^{-\alpha\lambda_s}~\sum_{n=0}^\infty\frac{1}{n!}\Big[\alpha\lambda_s\Big]^n\mathcal{T}_n(\beta)

where 

.. math::
  \mathcal{T}_0(\beta)=\frac{1}{2\pi}\int_{-\infty}^\infty\mathrm{e}^{i\beta t}~dt = \delta(\beta)

and 

.. math::
  \begin{align}
  \mathcal{T}_1(\beta)&=\frac{1}{\lambda_s}\int_{-\infty}^\infty P(\beta')~\mathrm{e}^{-\beta'/2}~\left[\frac{1}{2\pi}\int_{-\infty}^\infty\mathrm{e}^{i(\beta-\beta')t}~dt\right]~d\beta'\\
  &= \frac{1}{\lambda_s}P(\beta')~\mathrm{e}^{-\beta/2}. 
  \end{align}

In general subsequent :math:`\mathcal{T}_n(\beta)` terms can be obtained by convolving the first term with the previous one,

.. math::
  \mathcal{T}_n(\beta) = \int_{-\infty}^\infty \mathcal{T}_1(\beta')~\mathcal{T}_{n-1}(\beta-\beta')~d\beta'.

These :math:`\mathcal{T}_n(\beta)` follow the relationship

.. math:: 
  \mathcal{T}_n(\beta) = \mathrm{e}^{-\beta}~\mathcal{T}_n(-\beta)

and are normalized to unity,

.. math:: 
  \int_{-\infty}^\infty \mathcal{T}_n(\beta)~d\beta = 1.

This method is called the **phonon expansion method** because the :math:`n^{th}` term of this sum corresponds to the creation/destructin of :math:`n` phonons. Note that the :math:`n=0` term (which has that :math:`\mathcal{T}_0(\beta)=\delta(\beta)`) is carried forward separately. This is to ensure that if translational behavior is considered, then the elastic :math:`\beta=0` behavior will appear there. Thus, the continuous distribution contribution is approximated as 

.. math::
  S_s(\alpha,\beta) \approx \mathrm{e}^{-\alpha\lambda_s}~\sum_{n=1}^N\frac{1}{n!}\Big[\alpha\lambda_s\Big]^n\mathcal{T}_n(\beta)

\tiny and the zero-phonon term, 

.. math::
  \mathrm{e}^{-\alpha\lambda_s}~\delta(\beta)

is carried forward separately and discussed in :ref:`incoherent_elastic`.


.. either separately or in the translational calculation.


--------------------------------------


In LEAPR, the :math:`\mathcal{T}_n(-\beta)` functions are precomputed on the user-requested :math:`\beta` grid for :math:`n` extending up to some maximum value (default value of 100). These are used to obtain the :math:`S_s(\alpha,-\beta)`, which is converted to :math:`S_s(\alpha,\beta)` by multiplying by :math:`\mathrm{exp}(-\beta)`. 

The short-collision time approximation is used to obtain an effective temperature,

.. math:: 
  \overline{T}_s=\frac{T}{2\omega_s}~\int_{-\infty}^\infty\beta^2~P(\beta')~\mathrm{e}^{-\beta}~d\beta

where :math:`\omega_s` is the solid-type distribution weight.

--------------------------------------







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



Discrete Oscillator (Einstein Crystal)
----------------------------------------

Polyatomic molecules normally contain a number of vibrational modes that can be approximated as discrete oscillators. These would appear in the phonon distribution as a Dirac-:math:`\delta` functions with some corresponding weight, :math:`\omega_{i}\delta(\beta_i)`.

If there exist any peaks in the scattering law that the user wants to approximate as a :math:`\delta` function, the corresponding scattering law contribution :math:`S_d(\alpha,\beta)` can be computed as 

.. math::
  \begin{align}
  S_{i}(\alpha,\beta)&=\mathrm{e}^{-\alpha\lambda_i}\sum_{n=-\infty}^\infty\delta(\beta-n\beta_i)~I_n\left[\frac{\alpha\omega_i}{\beta_i\sinh(\beta_i/2)}\right]~\mathrm{e}^{-n\beta_i\,/2}\\
  &=\sum_{n=-\infty}^\infty A_{in}(\alpha)~\delta(\beta-n\beta_i)
  \end{align}

where the discrete oscillator Debye-Waller coefficient is defined as 

.. math:: 
  \lambda_i=\frac{\omega_i\,\coth(\beta_i/2)}{\beta_i}


.. _incoherent_elastic:

Incoherent Elastic Scattering
===============================

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



