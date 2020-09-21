

..
  COMMENT: .. contents:: Table of Contents

.. .. _inelastic_scattering:

.. Inelastic Scattering
.. ======================

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







