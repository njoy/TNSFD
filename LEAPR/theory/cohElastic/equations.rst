
..
  COMMENT: .. contents:: Table of Contents

Relevant Equations 
===============================


.. .. math::
  2d\sin(\theta) = n\lambda





.. Coherent scattering is when periodic constructive growth or destructive cancellation of the scattered waves occur. This is a difficult phenomena to model, and thus LEAPR is currently limited to describing elastic coherent scattering for the following materials:


The coherent elastic scattering cross section is defined as

.. math:: 
  \begin{gather}
  \sigma_{coh.el}(E,\mu)=\frac{\sigma_{coh}}{E}\sum_{E_i<E}f_i~\mathrm{e}^{-4W~E_i}~\delta(\mu-\mu_i)\\
  \mu_i = 1-\frac{E_i}{E}
  \end{gather}

where, when integrated over scattering cosine :math:`\mu` to remove angular dependence, becomes

.. math:: 
  \sigma_{coh.el}(E)=\frac{\sigma_{coh}}{E}\sum_{E_i<E}f_i~\mathrm{e}^{-4W~E_i}.


Here, we make use of the following definitions:

  :math:`\sigma_{coh}` 
    The effective bound coherent scattering cross section for the material

  :math:`W` 
    The effective Debye Waller coefficient (defined using the phonon distribution :math:`\rho(\beta)`) 

  .. math:: 
   \begin{gather}
    W = \frac{\lambda}{Ak_bT}\\~\\
    \lambda = \int_{-\infty}^\infty \frac{\rho(\beta)}{2\beta~\sinh(\beta/2)}~\mathrm{e}^{-\beta/2}~d\beta
   \end{gather}


  :math:`E_i` 
    The Bragg Edges

    .. math:: 
      E_i = \frac{\hbar^2\tau_i^2}{8m}

   where :math:`\tau_i` are the length of the vectors in one particular "shell" of the reciprocal lattice, and :math:`m` is the neutron mass. 


  :math:`f_i` 
    Factors related to the crystallographic structure factors by

    .. math::
      f_i = \frac{2\pi\hbar^2}{4mNV}\sum_{\tau_i}\Big|F(\tau)\Big|^2

    where the sum extends over all reciprocal lattice vectors of the given length and the crystallographic stucture factor is 

    .. math::
      \Big|F(\tau)\Big|^2= \left|\sum_{j=1}^N\mathrm{e}^{i2\pi\phi_j}\right|

    and :math:`N` is the number of atoms in the unit cell, :math:`\phi_j=\vec{\tau}\cdot\vec{\rho_j}` are the phases for the atoms, and :math:`\vec{\rho_j}` are the atomic positions.




Hexagonal Material Example - Graphite 
----------------------------------------

For hexagonal materials, the lattice is described by two constants :math:`a` and :math:`c`. The reciprocal lattice vector lengths are given by 

.. math::
   \left(\frac{\tau}{2\pi}\right) = \frac{4}{3a^2}\left(l_1^2+l_2^2+l_3^2\right)+\frac{1}{c^2}~l_3^2

where :math:`l_1`, :math:`l_2`, and :math:`l_3` run over all positive and negative integers (including zero). 

The volume of the unit cell is 

.. math::
  V=\frac{\sqrt{3}~a_2~c}{2}.

For graphite, there are four atoms in the unit cell at positions

.. math::
  \Big(0,0,0\Big)\quad\Big(-\frac{1}{3},\frac{1}{3},0\Big)\quad\Big(-\frac{2}{3},-\frac{1}{3},\frac{1}{2}\Big)\quad\Big(-\frac{1}{3},\frac{1}{3},\frac{1}{2}\Big)

These positions give the following phases:

.. math::
  \begin{align*}
    \phi_1 &= 0\\
    \phi_2 &= -\frac{1}{3}~l_1 + \frac{1}{3}~l_2     \\
    \phi_3 &= -\frac{2}{3}~l_1 - \frac{1}{3}~l_2 + \frac{1}{2} l_3\\
    \phi_4 &= -\frac{1}{3}~l_1 + \frac{1}{3}~l_2 + \frac{1}{2} l_3
  \end{align*}

and the form factor for graphite becomes 

.. math::
  |F|^2 = \begin{cases} 
      6+10~\cos\left(\frac{2\pi}{3}(l_1-l_2)\right) & l_3~\mbox{even}  \\
      4~\sin^2\left(\frac{\pi}{3}(l_1-l_2)\right) & l_3~\mbox{odd}
   \end{cases}


LEAPR contains similar logic to handle face-centered cubic (fcc), e.g. aluminum, and body-centered cubic (bcc), e.g. iron, lattices.




Multiple Atomic Species
------------------------

Preparing coherent elastic scattering data for materials containing different atomic species (e.g., beryllium oxide) poses additional difficulties. For such materials, the bound coherent scattering cross section and Debye-Waller factor vary from nuclide to nuclide, thus for the :math:`j^{th}` species are denoted as :math:`\sigma_j` and :math:`W_j`, respectively. Recall that the coherent elastic scattering cross section is written as 

.. math::
    \sigma_{coh.el}(E,\mu)=\frac{\sigma_c}{E}\sum_{E_i<E}f_i~\mathrm{e}^{-4W~E_i}~\delta(\mu-\mu_i)

where 

.. math:: 
  f_i = \frac{2\pi\hbar^2}{4mNV}\sum_{\tau_i}\Big|F(\tau)\Big|^2.

Since the bound coherent scattering cross section an the Debye-Waller factor differ according to the species of atom, the differential scattering cross section is written as 

.. math::
  \begin{align}
    \sigma_{coh.el}(E,\mu)&=\frac{\sigma_c}{E}\sum_{E_i<E}f_i~\mathrm{e}^{-4W~E_i}~\delta(\mu-\mu_i) \\
    &=\frac{1}{E}\sum_{E_i<E}\left[\sigma_{coh}~f_i~\mathrm{e}^{-4WE_i}\right]\delta(\mu-\mu_i)\\
    &=\frac{1}{E}\sum_{E_i<E}\left|\sum_{j=1}^N\sqrt{\sigma_j^{~}}~\mathrm{e}^{-2W_jE_i}~\mathrm{e}^{2i\pi\phi_j}\right|^2\delta(\mu-\mu_i)
  \end{align}



.. math::
  \sigma_{coh}~\mathrm{e}^{-4WE_i}~f_i=\left|\sum_{j=1}^N\sqrt{\sigma_j^{~}}~\mathrm{e}^{-2W_jE_i}~\mathrm{e}^{2i\pi\phi_j}\right|^2

The effective bound coherent scattering cross section for these materials is given by

.. math::
  \sigma_{coh} = \sum_{j=1}^{N}\sigma_j
  
Since LEAPR and THERMR only work with one material at a time, they don't have access to different values of :math:`W_j` for the atoms in the unit cell. Therefore, they assume that :math:`W_jE_i` is small (that :math:`W_j` does not vary much from site to site). This allows us to simplify 

























.. Since a prerequisite for coherent elastic scattering is spatial correlation of atomic sites, this type of scattering is not considered for amorphous solids or liquids, only regular repeating strucures (e.g. FCC, BCC, HCP, etc.). 

.. If a material is comprised of strong coherent scatterers (e.g. graphite) where there is strong spatial correlation between atomic sites (such as in a crystalline material), the scattered neutron waves from zero-phonon collisions can interfere, creating **coherent elastic scattering**. This scattering phenonema leads to "Bragg diffraction". 








.. The differential coherent elastic scattering cross section is given by 

.. .. math:: 
  \sigma_{coh.el}(E,\mu)=\frac{\sigma_c}{E}\sum_{E_i<E}f_i~\mathrm{e}^{-4WE_i}~\delta(\mu-\mu_i)

.. where 

.. .. math::
  \mu_i=1-\frac{E_i}{E}.

.. Furthermore, the integrated cross section is given by 

.. .. math:: 
  \sigma_{coh.el}(E)=\frac{\sigma_{coh}}{E}\sum_{E_i<E}f_i~\mathrm{e}^{-4WE_i}.

.. Here, :math:`\sigma_{coh}` is the effective bound scattering cross section for the material, :math:`E_i` are the "Bragg Edges", :math:`f_i` are related to the crystallographic structure factors, and 

  







