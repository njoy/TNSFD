.. This is a comment. Note how any initial comments are moved by
   transforms to after the document title, subtitle, and docinfo.

.. demo.rst from: http://docutils.sourceforge.net/docs/user/rst/demo.txt

.. |EXAMPLE| image:: _images/temp.png
   :width: 1em


**********************
Additional Resources
**********************

..
  COMMENT: .. contents:: Table of Contents

-------------------------------------------------------------------------------

.. _background_phonon_dos:

Vibrational Frequency Spectrum
==============================================
The vibrational frequency spectrum (also known as the phonon frequency spectrum and phonon density of states) is a function that represents the available vibrational modes in a material that can be excited. 


.. figure:: _images/ZrH_phononDOS.png
    :width: 90%
    :align: center

    The vibrational frequency spectrum for ZrH is shown.

The figure above shows the phonon density of states for zirconium hydride, ZrH. This shows the energies that a lattice vibration (phonon) could have, if they were to exist. When a thermal neutron collides with a material, it can collide elastically (interact with no phonons) or can collide inelastically (create or destroy phonons). A neutron will gain energy by destroying a phonon, or lose energy by creating a phonon. 

Note that most non-zero values for H in ZrH is centered about 0.14 eV, meaning that if phonons are excited in the material, they are likely to have an energy around 0.14 eV. So if a thermal neutron were to inelasticalyl scatter off of a hydrogen bound in ZrH, it would likely create a 0.14 eV phonon (thus losing 0.14 eV) or destroy a 0.14 eV phonon (thus gaining 0.14 eV). Similarly, it could create two phonons (thus losing about 0.28 eV) or destroy two phonons (thus gaining 0.28 eV). Regardless, we find that an inelastically scattered thermal neutron is likely to lose energy in multiples of about 0.14 eV, in this example. 

.. figure:: _images/ZrH_xs_mu_0p6.png
   :width: 100%
   :align: center


In fact, when considering the cross section obtained using the above phonon spectrum, we find that a neutron with initial energy 0.5 eV will likely lose integer multiples of about 0.14 eV, which indicate the creation of 1, 2, and 3 phonons. Note that destruction of 1 phonon (corresponding to a neutron gaining about 0.14 eV) can occur, butis less likely than phonon creation due to incoming neutron energy and material temperature. 


1. *So why is the phonon spectrum important for thermal neutron scattering?*

    Conservation of energy requires that any energy a neutron gains/loses must be met with a loss/gain of energy elsewhere. For thermal neutron scattering, this "elsewhere" is in lattice and molecular vibrations. So we need to know what lattice vibrations are preferred for a given material, as those indicate the increments of energy loss and gain that will be preferred for neutron energy exchange.


2. *Is the phonon distribution temperature dependent?*

    The phonon distribution shows what vibrational modes are *available* to be excited, not which ones *are currently* excited. So a material at 0 Kelvin has a phonon distribution. That being said, phonon distributions are temperature dependent, since increasing temperature results in thermal expansion which changes the preferred vibrations of the lattice. As temperatures increase, the phonon distributions tend to smooth out and shift to lower energies.




.. Debye-Waller Coefficient
.. ---------------------------
.. The Debye-Waller factor is used to describe th


.. Originally, in X-ray scattering by atoms in a crystal, the probability of coherent scattering was proportional to the Debye-Waller factor, and depended on the temperature of the crystal. So a really high DWF means that there is a lot of coherence in your system. o


.. The Debye-Waller factor has been seen as a relative probability of coherent vs. incoherent scattering, or of elastic vs. inelastic processes. However, these are not strictly correct and are only actually valid for a certain kinematic region. 



-------------------------------------------------------------------------------

.. _additional_phonon_expansion:

Phonon Expansion Method
===========================

As mentioned in :ref:`theory_incoherent_contin`, the scattering law equations that need be solved are 

.. math::
  S^{(s)}_{n.sym}(\alpha, \beta)=\frac{1}{2 \pi} \int_{-\infty}^{\infty} \mathrm{e}^{i \beta t} \mathrm{e}^{-\gamma(t)} d t

.. math::
    \gamma(t)=\alpha\lambda_s -\alpha \int_{-\infty}^\infty P(\beta')~\mathrm{e}^{-\beta'/2}~\mathrm{e}^{-i\beta' t}~d\beta'

.. math:: 
  P(\beta)=\frac{\rho(\beta)}{2\beta\sinh(\beta/2)}.

The :math:`\mathrm{exp}(-\gamma(t))` term in the scattering law can be approximated using a Taylor series. Since the Taylor expansion of an exponential is

.. math:: 
   \mathrm{e}^{x} = \sum_{n=0}^\infty \frac{x^n}{n!}

the exponential :math:`\gamma(t)` term becomes


.. math::
  \mathrm{e}^{-\gamma(t)} = \sum_{n=0}^\infty\left(\mathrm{e}^{-\alpha\lambda_s}\frac{1}{n!} \left[\alpha\int_{-\infty}^{\infty}P(\beta')\mathrm{e}^{-\beta'/2}\mathrm{e}^{-i\beta't}~d\beta'\right]^n\right).

This representation is used in the :math:`S(\alpha,\beta)` definition 

.. math::
  \begin{align*}
  S^{(s)}_{n.sym}(\alpha,\beta,T)=&\frac{1}{2\pi}\int_{-\infty}^{\infty}\mathrm{e}^{i\beta t}\sum_{n=0}^\infty\left(\mathrm{e}^{-\alpha\lambda_s}\frac{1}{n!}\left[\alpha\int_{-\infty}^{\infty}P(\beta')\mathrm{e}^{-\beta'/2}\mathrm{e}^{-i\beta't}~d\beta'\right]^n\right)~dt\\
                                =~&\mathrm{e}^{-\alpha\lambda_s}\sum_{n=0}^\infty\frac{\alpha^n}{n!}\frac{1}{2\pi}\int_{-\infty}^{\infty}\mathrm{e}^{i\beta t}\left[\int_{-\infty}^{\infty}P(\beta')\mathrm{e}^{-\beta'/2}\mathrm{e}^{-i\beta't}~d\beta'\right]^n~dt\\
                                =~&\mathrm{e}^{-\alpha\lambda_{s}}\sum_{n=0}^{\infty}\frac{1}{n!}\left[\alpha\lambda_{s}\right]^{n}\mathcal{T}_{n}(\beta)
  \end{align*}


where :math:`\mathcal{T}_n(\beta)` is defined as 

.. math:: 
  \lambda_s^n\mathcal{T}_n(\beta)=\frac{1}{2\pi}\int_{-\infty}^{\infty}\mathrm{e}^{i\beta t}\left[\int_{-\infty}^{\infty}P(\beta')\mathrm{e}^{-\beta'/2}\mathrm{e}^{-i\beta't}~d\beta'\right]^n~dt.

Note that in this above definition, 

.. math:: 
  \mathcal{T}_0(\beta)=\frac{1}{2\pi}\int_{-\infty}^\infty\mathrm{e}^{i\beta t}~dt = \delta(\beta)

and 

.. math::
  \mathcal{T}_{1}(\beta)=\int_{-\infty}^{\infty} \frac{P_{s}(\beta')~\mathrm{e}^{-\beta' / 2}}{\lambda_{s}}\left\{\frac{1}{2 \pi} \int_{-\infty}^{\infty} \mathrm{e}^{i(\beta-\beta') t}~d t\right\} d \beta'=\frac{P_{s}(\beta)~\mathrm{e}^{-\beta / 2}}{\lambda_{s}}





-------------------------------------------------------------------------------

.. _additional_discrete_oscillator:

Discrete Oscillator Method
==============================

Recall from :ref:`theory_incoherent_contin` that definition of the non-symmetric scattering law (in the incoherent and Gaussian approximations) is 

.. math::
  S_{n.sym}(\alpha,\beta,T)=\frac{1}{2\pi}\int_{-\infty}^{\infty}\mathrm{e}^{i\beta t }\mathrm{e}^{-\gamma( t )}~d t 


.. math::
  \gamma( t )=\alpha\int_{-\infty}^{\infty}P(\beta)\left[1-\mathrm{e}^{-i\beta t }\right]\mathrm{e}^{-\beta/2}~d\beta


.. math::
  P(\beta)=\frac{\rho(\beta)}{2\beta\sinh(\beta/2)}.

:math:`\gamma(t)` can be separated into two terms, yielding

.. math::
  \gamma( t )= \alpha\int_{-\infty}^\infty P(\beta')\mathrm{e}^{-\beta'/2}~d\beta                                      -\alpha\int_{-\infty}^\infty P(\beta')\mathrm{e}^{-i\beta' t } \mathrm{e}^{-\beta'/2}~d\beta'.

Note that :math:`\rho(\beta)` is an even function in :math:`\beta`, and so since :math:`P(\beta)` is defined as an even function divided by the product of two odd functions, :math:`P(\beta)` is even as well. This fact allows us to conveniently collapse the first integral to only extend from :math:`0\rightarrow\infty`,

.. math::
  \gamma( t )= \alpha\int_{0}^\infty P(\beta') \left[\mathrm{e}^{\beta'/2}+\mathrm{e}^{-\beta'/2}\right] ~d\beta                                      -\alpha\int_{-\infty}^\infty P(\beta')\mathrm{e}^{-i\beta' t } \mathrm{e}^{-\beta'/2}~d\beta'.
      
By inserting the definition of :math:`P(\beta)`, this first term can be further amended to,

.. math:: 
  \gamma( t )= \alpha\left[\int_{0}^\infty \frac{\rho(\beta')}{\beta'}~\coth(\beta'/2)~d\beta'                                      -\int_{-\infty}^\infty P(\beta')\mathrm{e}^{-i\beta' t } \mathrm{e}^{-\beta'/2}~d\beta'\right].

We repeat this process with the latter term.

.. math::
  \begin{align}
    \int_{-\infty}^\infty P(\beta')\mathrm{e}^{-i\beta' t -\beta'/2}~d\beta' 
    &=\int_{0}^\infty P(\beta')
      \left[\mathrm{e}^{ i\beta' t } \mathrm{e}^{ \beta'/2} +
      \mathrm{e}^{-i\beta' t } \mathrm{e}^{-\beta'/2}\right]~d\beta'\\
    &=\int_{0}^\infty P(\beta')
      \Big[\big(\cos(\beta' t )+ i\sin(\beta' t )\big)\mathrm{e}^{~\beta'/2}+\big(\cos(\beta' t )-i\sin(\beta' t )\big)\mathrm{e}^{-\beta'/2}\Big] ~d\beta'\\
    &= \int_0^\infty P(\beta')2\Big[\cos(\beta' t )\cosh\left(\beta'/2\right)+
       i\sin(\beta' t )\sinh\left(\beta'/2\right)\Big]~d\beta',
  \end{align}

Recall that :math:`\cosh(x)=\cos(ix)` and :math:`\sinh(x)=-i\sin(ix)`, as well as that :math:`\cos(a+b)=\cos(a)\cos(b)-\sin(a)\sin(b)`. Applying these definitions allows the bracketed part of the integrand to be rewritten as

.. math::
	    \begin{align}
	        \cos(\beta' t )\cosh\left(\beta'/2\right)+
	          i\sin(\beta' t )\sinh\left(\beta'/2\right)
	        =&\cos(\beta' t )\cos\left(\beta'i/2\right)+
	          i\sin(\beta' t )(-i)\sin\left(\beta'i/2\right) \\
	        =&\cos(\beta' t )\cos\left(\beta'i/2\right)+
	          \sin(\beta' t )\sin\left(\beta'i/2\right) \\
	        =&\cos(\beta'( t -i/2)).
	    \end{align}


This simplification allows us to create a simpler expression for :math:`\gamma( t )`,

.. math::
  \gamma( t )= \alpha\left[\int_{0}^\infty \frac{\rho(\beta')}{\beta'}~\coth(\beta'/2)~d\beta'                                      -\int_0^\infty \frac{\rho(\beta')}{\beta'\sinh(\beta'/2)}~\cos(\beta'( t -i/2))~d\beta'\right].

Note that thus far, this is simply a rewrite of the continuous equations that were stated in :ref:`theory_incoherent_contin` - *no further assumptions have been made on the frequency distribution :math:`\rho(\beta)`*. At this point, howver, we will assume that the frequency distributions consists only of a single Dirac-:math:`\delta` function, an discrete oscillator located at :math:`\beta=\beta_i` (i.e. :math:`\rho(\beta)=\delta(\beta-\beta_i)`). This allows for a simple removal of the :math:`\beta'` integrals,

.. math::
  \gamma( t )= \frac{\alpha\coth(\beta_i/2)}{\beta_i} -\frac{\alpha\cos(\beta_i( t -i/2))}{\beta_i\sinh(\beta_i/2)}

which, when plugged into the scattering law definition, yields 

.. math::
  \begin{align}
			S_{n.sym}(\alpha,\beta,T)
			&=\frac{1}{2\pi}\int_{-\infty}^{\infty}\mathrm{e}^{i\beta t }\mathrm{exp}\left[-\frac{\alpha\coth(\beta_i/2)}{\beta_i}                                                        +\frac{\alpha\cos(\beta_i( t -i/2))}{\beta_i\sinh(\beta_i/2)}\right] ~d t \\
			&=\mathrm{e}^{-\alpha\lambda_i}\frac{1}{2\pi}\int_{-\infty}^{\infty}\mathrm{e}^{i\beta t }\mbox{exp}\left[                                                        \frac{\alpha\cos(\beta_i( t -i/2))}{\beta_i\sinh(\beta_i/2)}\right] ~d t \label{eq:beforeBesselFunction}\\
			&=\mathrm{e}^{-\alpha\lambda_i}\frac{1}{2\pi}\int_{-\infty}^{\infty}\mathrm{e}^{i\beta t }\sum_{n=-\infty}^\infty\mathrm{I}_n\left(\frac{\alpha}{\beta_i\sinh(\beta_i/2)}\right) \mathrm{e}^{-ni(\beta_i t -i\beta_i/2)}~d t \\
			&=\mathrm{e}^{-\alpha\lambda_i}\sum_{n=-\infty}^\infty\mathrm{I}_n\left(\frac{\alpha}{\beta_i\sinh(\beta_i/2)}\right)\mathrm{e}^{-n\beta_i/2}\frac{1}{2\pi}\int_{-\infty}^{\infty}\mathrm{e}^{i\beta t } \mathrm{e}^{-ni\beta_i t }~d t \\
			&=\mathrm{e}^{-\alpha\lambda_i}\sum_{n=-\infty}^\infty\mathrm{I}_n\left(\frac{\alpha}{\beta_i\sinh(\beta_i/2)}\right)\mathrm{e}^{-n\beta_i/2}\delta(\beta-n\beta_i)\tag{\ref{eq:longDeltaFunctionSAB}}.
		\end{align}

Note that the first term in :math:`\gamma(t)` is represented as :math:`-\alpha\lambda_i` - this use of the Debye-Waller factor is consistent with the notation used in the continuous case. 

Another piece of interest is that the Bessel function of the first kind :math:`\mathrm{I}_n(x)` in put in place of the large exponential, as is consistent with its definition,

.. math::
		    \mathrm{e}^{x\,\cos(\theta)}=\sum_{n=-\infty}^\infty \mathrm{I}_n(x)~\mathrm{e}^{-in\theta}.


Thus, the single discrete oscillator contribution to the scattering law that is presented in :ref:`theory_incoherent_discre` has been retrieved. 







