
**********************
Theory
**********************

..
  COMMENT: .. contents:: Table of Contents

Overview
=====================

In the incoherent approximation, the thermal scattering cross section is defined as 

.. math::
    \sigma(E\rightarrow E',\mu) = \frac{\sigma_b}{k_bT}\sqrt{\frac{E'}{E}}~S(\alpha,\beta)
 
where :math:`S(\alpha,\beta)` is the thermal scattering law. The purpose of LEAPR is to prepare the scattering law (along with Bragg edges, Debye-Waller factors, etc.) for further use by supplementary codes like the THERMR module. 


As mentioned in [LINK TO THERMAL SCATTERING DATA], thermal neutron scattering can be categorized as either elastic or inelastic, both of which can have coherent and incoherent contributions. Modern thermal scattering data processing typically combines coherent inelastic with incoherent inelastic in what is called the incoherent approximation.


With this approximation, NJOY is prepared to handle the following thermal scattering types:

.. Typically, thermal scattering is divided into the following categories:

1. **Incoherent elastic**
   This is important for hydrogeneous solids like solid methane, polyethylene, and zirconium hydride. 
2. **Coherent elastic**
   This is important for crystalline solids such as graphite and Beryllium. LEAPR prepares the locations of the Bragg edges and their weights. 
3. **Inelastic scattering** (in the incoherent approximation)
   This is important for all materials. To describe this data, LEAPR needs to prepare the scattering law :math:`S(\alpha,\beta)`, and does so with the phonon density of states. The phonon distribution can be decomposed into three components: a solid-type continuous contribution, a discrete-oscillator contribution, and a translational contribution.




These three components of the phonon distribution will be further described now.

.. How NJOY handles these three types of scattering will be explained in subsequent sections.


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
  S^{(J)}(\alpha,\beta) = \int_{-\infty}^\infty S^{(J)}(\alpha,\beta')~S^{(J-1)}(\alpha,\beta-\beta')~d\beta'


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






Continuous, Solid-type Spectrum
-------------------------------

For a solid-type spectrum, the scattering law is defined as 

 .. math::
     S(\alpha,\beta) = \frac{1}{2\pi}\int_{-\infty}^\infty\mathrm{e}^{i\beta t}~\mathrm{e}^{\gamma(t)-\gamma(0)}~dt

.. math::
    \gamma(t)=\alpha\int_{-\infty}^\infty \frac{\rho(\beta)}{2\beta\sinh(\beta/2)}~\mathrm{e}^{-i\beta t}~\mathrm{e}^{-\beta/2}~d\beta

where the phonon distribution :math:`\rho(\beta)` is normalized to one

.. math::
  \int_0^\infty\rho(\beta)~d\beta=1.

Recall that while :math:`\beta` is defined as unitless energy change :math:`(E'-E)/k_bT`, the input phonon distribution must be provided energy exchange :math:`E'-E` in units of eV.

.. Recall that :math:`\beta` is unitless neutron energy exchange

.. .. math::
  \beta=\frac{E'-E}{k_bT}

.. Although the phonon distribution :math:`\rho(\beta)` is shown as a function of :math:`\beta`, it is given to LEAPR as a function of energy exchange :math:`|E'-E|` (in eV).

.. Although the phonon distribution is used here as a function of :math:`\beta`, it will be provided as a function of energy,

The Debye-Waller coefficient is defined as 

.. math::
  \lambda_s = \int_{-\infty}^\infty \frac{\rho(\beta)}{2\beta\sinh(\beta/2)}~\mathrm{e}^{-\beta/2}~d\beta

which simplifies the scattering law :math:`S(\alpha,\beta)` to be 

 .. math::
     S(\alpha,\beta) = \frac{1}{2\pi}\mathbf{e}^{-\alpha\lambda_s}\int_{-\infty}^\infty\mathrm{e}^{i\beta t}~\mathrm{e}^{\gamma(t)}~dt

**Phonon Expansion**

The exponential of :math:`\gamma(t)` is a complex and highly oscillatory. 

.. math::
  \mathrm{e}^{\gamma(t)}=\mathrm{exp}\left[ \alpha\int_{-\infty}^\infty \frac{\rho(\beta)}{2\beta\sinh(\beta/2)}~\mathrm{e}^{-i\beta t}~\mathrm{e}^{-\beta/2}~d\beta  \right]\\

To ease the burden of calculating the scattering law, LEAPR uses the phonon expanion method, which involves expanding the :math:`\gamma(t)` exponential as a Taylor series, 

.. math::
   \mathrm{e}^{\gamma(t)} =\sum_{n=0}^\infty\frac{1}{n!}\left[ \alpha\int_{-\infty}^\infty \frac{\rho(\beta)}{2\beta\sinh(\beta/2)}~\mathrm{e}^{-i\beta t}~\mathrm{e}^{-\beta/2}~d\beta  \right]^n

which, when used in the solid-type scattering law definition, results in

.. .. math::
..      S(\alpha,\beta) = \frac{1}{2\pi}\mathbf{e}^{-\alpha\lambda_s} \sum_{n=0}^\infty\int_{-\infty}^\infty\mathrm{e}^{i\beta t}~\frac{1}{n!}\left[ \alpha\int_{-\infty}^\infty \frac{\rho(\beta)}{2\beta\sinh(\beta/2)}~\mathrm{e}^{-i\beta t}~\mathrm{e}^{-\beta/2}~d\beta  \right]^n~dt.

.. The order of summation and integral can swapped, and 

.. math::
  \begin{align}
     S(\alpha,\beta) =~&\mathbf{e}^{-\alpha\lambda_s} \sum_{n=0}^\infty \frac{1}{n!}\alpha^n \\
     \times~&\frac{1}{2\pi} \int_{-\infty}^\infty\mathrm{e}^{i\beta t}~\left[ \int_{-\infty}^\infty \frac{\rho(\beta)}{2\beta\sinh(\beta/2)}~\mathrm{e}^{-i\beta t}~\mathrm{e}^{-\beta/2}~d\beta  \right]^n~dt
  \end{align}

(note that the order of summation and integral have been swapped). Now, the second line of the above equation is redefined as :math:`\lambda_s^n\mathcal{T}_n(\beta)`. This allows for the solid-type scattering law to be redefined as 

.. math::
  S(\alpha,\beta) = \mathrm{e}^{-\alpha\lambda_s}~\sum_{n=0}^\infty\frac{1}{n!}\Big[\alpha\lambda_s\Big]^n\mathcal{T}_n(\beta)

where 

.. math::
  \mathcal{T}_0(\beta)=\frac{1}{2\pi}\int_{-\infty}^\infty\mathrm{e}^{i\beta t}~dt = \delta(\beta)

and 

.. math::
  \begin{align}
  \mathcal{T}_1(\beta)&=\frac{1}{\lambda_s}\int_{-\infty}^\infty \frac{\rho(\beta')}{2\beta'\sinh(\beta'/2)}~\mathrm{e}^{-\beta'/2}~\left[\frac{1}{2\pi}\int_{-\infty}^\infty\mathrm{e}^{i(\beta-\beta')t}~dt\right]~d\beta'\\
  &= \frac{1}{\lambda_s}\frac{\rho(\beta)}{2\beta\sinh(\beta/2)}~\mathrm{e}^{-\beta/2}. 
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

In LEAPR, the :math:`\mathcal{T}_n(-\beta)` functions are precomputed on the user-requested :math:`\beta` grid for :math:`n` extending up to some maximum value (default value of 100). These are used to obtain the :math:`S(\alpha,-\beta)`, which is converted to :math:`S(\alpha,\beta)` by multiplying by :math:`\mathrm{exp}(-\beta)`. 





Discrete Oscillator (Einstein Crystal)
----------------------------------------



Translational/Diffusive Behaviour
-----------------------------------





.. The LEAPR module is used to prepare the thermal scattering law :math:`S(\alpha,\beta)`, which describes thermal scattering from bound moderators. 

.. LEAPR uses the incoherent approximation for preparing the thermal scattering data. 




