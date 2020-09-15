
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








