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






