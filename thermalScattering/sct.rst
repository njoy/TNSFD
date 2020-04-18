.. This is a comment. Note how any initial comments are moved by
   transforms to after the document title, subtitle, and docinfo.

.. demo.rst from: http://docutils.sourceforge.net/docs/user/rst/demo.txt

.. |EXAMPLE| image:: _images/temp.png
   :width: 1em

.. .. .. _theory:

**************************************
Short-Collision Time Approximation
**************************************

..
  COMMENT: .. contents:: Table of Contents


When calculating the contribution of incoherent scattering via use of the *phonon expansion*, values corresponding to significant change in momentum (i.e. large :math:`\alpha` values) can become costly to calculate. To avoid prohibitively costly calculations, LEAPR employs the **short-collision time approximation (SCT)** to describe scattering in a solid for these conditions of large momentum transfer. The SCT approximation is defined as 

.. math::
  S(\alpha,-\beta)=\frac{1}{\sqrt{4\pi\alpha w_s \overline{T}/T}}~\mathrm{exp}\left[-\frac{(\alpha w_s-\beta)^2}{\alpha w_s\overline{T}/T}\right]
  
and

.. math::
  S(\alpha,\beta)=\mathrm{e}^{-\beta}~S(\alpha,\beta)


where the effective temperature :math:`\overline{T}` is defined as 

.. math:: 
  \overline{T}=\frac{T}{2w_s}\int_{-\infty}^\infty\beta^2P(\beta)\mathrm{e}^{-\beta}~d\beta

and :math:`w_s` is the weight for the continuous, solid-type spectrum.


.. The SCT approximation is found to work "well for large incident neutron energies when the duration of a collision is short compared with the natural periods of atomic motion" [https://digital.library.unt.edu/ark:/67531/metadc1089525/m2/1/high_res_d/5508404.pdf] [THE SHORT COLLISION TIME APPROXIMATION FOR NEUTRON SCATTERING USING DISCRETE FREQUENCY DISTRIBUTION by Ryskamp]  "For large incident neutron energies the duration of a collison is short compared with the natural periods of atomic motion."


