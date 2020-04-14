.. This is a comment. Note how any initial comments are moved by
   transforms to after the document title, subtitle, and docinfo.

.. demo.rst from: http://docutils.sourceforge.net/docs/user/rst/demo.txt

.. |EXAMPLE| image:: _images/temp.png
   :width: 1em

.. _coh_elastic:

**************************************
Coherent Elastic Scattering
**************************************

.. COMMENT: .. contents:: Table of Contents



.. _coherent_elastic:

Overview
==============================================

Coherent scattering is when periodic constructive growth or destructive cancellation of the scattered waves occur. This is a difficult phenomena to model, and thus LEAPR is currently limited to describing elastic coherent scattering for the following materials:

  +-----------------+------------------------------+
  | Materials       | Crystalline Structure        |
  +=================+==============================+
  | Graphite        | Hexagonal                    |
  +-----------------+------------------------------+
  | Beryllium Metal | Hexagonal Close-Packed (HCP) |
  +-----------------+------------------------------+
  | Beryllium Oxide | Inter-penetrating HCP        |
  +-----------------+------------------------------+
  | Aluminum        | Face-Centered Cubic (FCC)    |
  +-----------------+------------------------------+
  | Lead            | Face-Centered Cubic (FCC)    |
  +-----------------+------------------------------+
  | Iron            | Body-Centered Cubic (BCC)    |
  +-----------------+------------------------------+



The differential coherent scattering cross section is

.. math:: 
  \sigma_{coh}(E,\mu)=\frac{\sigma_c}{E}\sum_{E_i<E}f_i~\mathrm{e}^{-4W~E_i}~\delta(\mu-\mu_i)

where :math:`W` is the effevtive Debye-Waller coefficient, :math:`\sigma_c` is the bound coherent scattering cross section. :math:`E_i` are Bragg Edges, defined in term


  +-------------------+-----------------------+------------------------------------+
  | Symbol            | Name                  |  Formula                           |
  +===================+=======================+====================================+
  | :math:`W`         | | Effective Debye     |                                    |
  |                   | | Waller coefficient  |                                    |
  +-------------------+-----------------------+------------------------------------+
  | :math:`\sigma_c`  | | Bound coherent      |                                    |
  |                   | | scattering cross    |                                    |
  |                   | | section             |                                    |
  +-------------------+-----------------------+------------------------------------+
  | :math:`E_i`       | | Bragg Edges         | :math:`E_i=                        |
  |                   |                       | \frac{\hbar^2\tau_i^2}{8m}`        |
  +-------------------+-----------------------+------------------------------------+
  | :math:`\tau_i`    | | Length of the       |                                    |
  |                   | | :math:`i^{th}`      |                                    |
  |                   |   reciprocal          |                                    |
  |                   | | lattice vector      |                                    |
  +-------------------+-----------------------+------------------------------------+
  | :math:`f_i`       |                       | :math:`f_i=                        |
  |                   |                       | \frac{2\pi\hbar^2}{4mNV}           |
  |                   |                       | \sum_{\tau_i}\Big|F(\tau)          |
  |                   |                       | \Big|^2`                           |
  +-------------------+-----------------------+------------------------------------+
  | | :math:`\Big|    | | Crystallographic    | :math:`|F(\tau)|^2                 |
  |   F(\tau)\Big|^2` | | structure           | = \left|\sum_{j=1}^N               |
  |                   | | factor              | \mathrm{e}^{2\pi\phi_ji}\right|^2` |
  +-------------------+-----------------------+------------------------------------+



.. math::
  \sigma_l=\frac{\sigma_{coh}\lambda^2}{2\sqrt{3}a^2c}\sum_{\tau}^{\tau\leq4\pi/\lambda}\frac{m_{\tau}}{\tau}\mathrm{exp}\left[-\frac{\hbar^2\tau^2}{2M}\int_0^{\omega_{\max}}\frac{\rho(\omega)}{\omega}\mathrm{coth}\left(\frac{\omega}{k_bT}\right)\right]\frac{\left|F\right|^2}{N}

.. math::
  \tau^2=4\pi\left[\frac{4}{3}a^2\big(l_1^2+l_2^2+l_1l_2\big)+\frac{l_3^2}{c}\right] 

where :math:`N` is the number of atoms per unit cell, :math:`\sigma_{coh}` is the coherent scattering cross section, :math:`m_\tau` is the number of :math:`l_1,l_2,l_3` combinations that give a reciprocal lattice vector :math:`\tau` of equal magnitude.of equal magnitude.
:math:`|F|^2` is the form factor of the crystal, and :math:`a,c` are the magnitudes of the lattice vectors. 



For hexagonal lattices,

.. math::
  \left(\frac{\tau}{2\pi}\right)^2 = \left(\frac{4}{3}~a^2\right)~\Big(l_1^2+l_2^2+l_1l_2\Big) + \frac{l_3^2}{c^2}
  

:math:`f_i` are defined in terms of the crystallographic structure factors :math:`F`.



  

Hexagonal Lattices
-------------------------
LEAPR's treatment of hexagonal lattices is heavily influenced from the HEXSCAT code. Summary of the theory will be presented here.

Hexagonal Close Packed
-------------------------

Face Centered Cubic
--------------------------------------

Body Centered Cubic
---------------------


