.. This is a comment. Note how any initial comments are moved by
   transforms to after the document title, subtitle, and docinfo.

.. demo.rst from: http://docutils.sourceforge.net/docs/user/rst/demo.txt

.. |EXAMPLE| image:: _images/temp.png
   :width: 1em

.. .. .. _theory:

***********************************************
Coherent Inelastic Approximations
***********************************************

Vineyard Approximation
========================

.. While preparing the scattering law (for inelastic thermal scattering processes), it is standard to use the incoherent approximation. As introduced in :ref:`incoherent_approximation`, the incoherent approximation neglects the distinct contribution of the pair distribution function, which neglects interference between different atoms. In reality, however, scattered from different molecules do interfere, which results when there is a correlation between the positions of nearby molecules. This kind of coherence is described by the "static structure factor" :math:`S(\kappa)`. This quantity can be used the **Vineyard Approximation**,

.. .. math::
  \frac{\partial^2\sigma}{\partial\Omega\partial\epsilon}=\frac{\partial^2\sigma_{coh}}{\partial\Omega\partial\epsilon}~S(\kappa)+\frac{\partial^2\sigma_{incoh}}{\partial\Omega\partial\epsilon}

.. As mentioned in :ref:`inelastic`, typical inelastic calculations assume that the nuclear spins are randomly oriented. For some materials (e.g., cold hydrogen or cold deuterium), there 




.. The incoherent approximation is used while preparing the scattering law for inelastic thermal scattering collisions. 

While preparing the scattering law (for inelastic thermal scattering processes), it is standard to use the incoherent approximation. As introduced in :ref:`incoherent_approximation`, the incoherent approximation neglects the distinct contribution of the pair distribution function, which neglects interference between different atoms. 

Intermolecular interference occurs when there is both a significant bound coherent scattering cross section (property of the atoms) as well as some correlation between the positions of nearby molecules (property of the lattice). If these requirements are met, coherent scattering may become non-negligible, at which point its effect can be accounted for by using the **Vineyard** approximation. 



.. In reality, however, scattered from different molecules do interfere, which results when there is a correlation between the positions of nearby molecules. This kind of coherence is described by the "static structure factor" :math:`S(\kappa)`. This quantity can be used the **Vineyard Approximation**,


.. , which is made while using the continuous, translational, and discrete oscillator methods, ignores coherent effects. There are some material, however, in which scattered neutron waves can interfere with each other in meaningful ways. This inter-molecular coherence occurs when there is both a significant bound coherent scattering cross section (property of the atoms) as well as some correlation between the positions of nearby molecules (property of the lattice). If these requirements are met, coherent scattering may become non-negligible, at which point its effect can be accounted for by using the **Vineyard** or **Skold** approximations. 

Here, the scattering law is separated into a coherent and an incoherent contribution, which are weighted using a *coherent fraction* :math:`c`. The incoherent contribution to the scattering law can be obtained using the phonon density of states (which is explained more further in [LINK TO LEAPR DOCUMENTATION HERE]), but the coherent contribution must be approximated.

.. math:: 
  S(\alpha,\beta)=\big(1-c\big)S_{inc}(\alpha,\beta)+c~S_{coh}(\alpha,\beta)


The Skold approximation approximates the coherent scattering law by using the *static structure factor* :math:`S(\kappa)` to modify the incoherent scattering law.

.. math:: 
  S_{coh}(\alpha,\beta)=S_{inc}\left(\frac{\alpha}{S(\kappa)},\beta\right)\times S(\kappa)

The static structure factor :math:`S(\kappa)` is a user-provided input that describes correlation in molecular positions, where :math:`\kappa` is wave number, defined as 

.. math:: 
  \kappa = \frac{\sqrt{2Mk_bT\alpha}}{\hbar}


where :math:`M` is the mass of the scatterer. Using these relations, the coherent-corrected scattering can be obtained by solving the above three equations for all :math:`\alpha,\beta` values.









Cold Hydrogen and Deuterium 
-------------------------------
In !!!!!!!!!!!!, we made the assumption that spins are randomly distributed. This approximation is valid for most materials, but breaks down when describing liquid hydrogen and deuterium. To correct this error, quantum mechanical treatment is required to account for spin-spin correlations for atoms in the same molecule/structure.

For the remainder of this discussion, "hydrogen" will refer to the element, i.e. both :math:`^1\mathrm{H}` and :math:`^2\mathrm{D}`. 

For describing the spin-spin correlation for hydrogen, two cases are considered: *ortho* and *para*. Ortho hydrogen indicates that the spins of the nuclei are in the same direction, whereas para hydrogen indicates that the spins are in opposite direction.


.. figure:: _images/orthoVsPara.png
    :width: 40%
    :align: center

    Ortho and para describe the alignment of the spins that can occur in a pair of hydrogens. Ortho corresponds to the spins going in the same direction, whereas para corresponds to them going in the opposite direction. 


There are two different scattering law equations that describe cold hydrogen scattering, depending on the relative spin directions (ortho and para).


.. math::
  S_{n.sym}^{ortho}(\alpha,\beta)=\sum_{J~odd} \frac{P_J4\pi}{\sigma_b}\Big[ A_{ortho}\sum_{J'~even}F(J,J') + B_{ortho}\sum_{J'~odd} F(J,J') \Big]

.. math::
  S_{n.sym}^{para}(\alpha,\beta)=\sum_{J~even} \frac{P_J4\pi}{\sigma_b}\Big[ A_{para}\sum_{J'~even}F(J,J') + B_{para}\sum_{J'~odd} F(J,J') \Big]

.. math::
  F(J,J')=\big(2J'+1\big)~S_f(\omega\alpha,\beta+\beta_{JJ'})\sum_{l=\left|J'-J\right|}^{J'+J}4j_l^2(y)C^2(JJ'l;00)

Here you go

  +-------------------+---------------------------+------------------------------------+
  | Symbol            | Name                      |  Other Definition                  |
  +===================+===========================+====================================+
  | | :math:`A        | | Summation               | | Defined in the table below as    |
  |   _{ortho,para}`  |   coefficients            | | a function of :math:`a_c`        |
  | | :math:`B        |                           |   and :math:`a_i`                  |
  |   _{ortho,para}`  |                           |                                    |
  +-------------------+---------------------------+------------------------------------+
  | :math:`a_c` and   | | Coherent and incoherent | | Related to the coherent,         |
  | :math:`a_i`       | | scattering lengths      | | incoherent, and total bound      |
  |                   |                           | | scattering cross sections via    |
  |                   |                           | | :math:`\sigma_c=4\pi a_c^2\quad` |
  |                   |                           |   :math:`\sigma_i=4\pi a_i^2`      |
  |                   |                           | | :math:`\sigma_b=\sigma_c+\sigma_i|
  |                   |                           |   =4\pi\big(a_c^2+a_i^2\big)`      |
  +-------------------+---------------------------+------------------------------------+
  | :math:`P_J`       | | Statistical weight      |                                    |
  |                   | | factor                  |                                    |
  +-------------------+---------------------------+------------------------------------+
  | :math:`\beta      | | Energy transfer for a   | | :math:`\beta_{JJ'}=              |
  | _{JJ'}`           | | rotational transition   |  (E_{J'}-E_J)/k_bT`                |
  +-------------------+---------------------------+------------------------------------+
  | :math:`j_l(x)`    | | Spherical Bessel        |                                    |
  |                   | | function of order       |                                    |
  |                   |   :math:`l`               |                                    |
  |                   |                           |                                    |
  +-------------------+---------------------------+------------------------------------+
  | | :math:`C(       | | Clebsch-Gordan          |                                    |
  |   JJ';00)`        | | coefficient factor      |                                    |
  +-------------------+---------------------------+------------------------------------+
  | :math:`y`         |                           | | :math:`y=\kappa a/2`             |
  |                   |                           | | :math:`y=a                       |
  |                   |                           |   \sqrt{4Mk_bT\alpha/8}`           |
  +-------------------+---------------------------+------------------------------------+
  | :math:`a`         | | Interatomic distance    |                                    |
  |                   | | in the molecule         |                                    | 
  +-------------------+---------------------------+------------------------------------+
  | :math:`\omega_t`  | | Translational weight    | | :math:`1/2` for                  |
  |                   |                           |   :math:`^1\mathrm{H}` and         |
  |                   |                           |   :math:`1/4` for                  |
  |                   |                           |   :math:`^2\mathrm{D}`             |
  +-------------------+---------------------------+------------------------------------+
  | :math:`S_f        | | Free gas scattering law | | :math:`S_f(\alpha,\beta)=\frac{1}|
  | (\alpha,\beta)`   |                           |   {\sqrt{4\pi\omega_t\alpha}}      |
  |                   |                           |   \mathrm{exp}\left[-\frac{        |
  |                   |                           |   (\omega_t\alpha+\beta)^2}        |
  |                   |                           |   {4\omega_t\alpha}\right]`        |
  +-------------------+---------------------------+------------------------------------+




.. note::
  The summation coefficients :math:`A_{ortho,para}` and :math:`B_{ortho,para}` are provided for the relative materials in the table below. Here, :math:`a_c` and :math:`a_i` are the coherent and incoherent scattering lengths [#f1]_ .

  +--------------------+-------------------+------------------------+-------------------+-------------------+
  | **Spin Alignment** | :math:`^1\mathrm{H}`                       | :math:`^2\mathrm{D}`                  |
  +====================+===================+========================+===================+===================+
  |                    | :math:`A` (even)  | :math:`B` (odd)        | :math:`A` (even)  | :math:`B` (odd)   |
  +--------------------+-------------------+------------------------+-------------------+-------------------+
  | **Ortho**          | :math:`a_c^2/3`   | :math:`a_c^2+2a_i^2/3` | :math:`a_c^2      | :math:`3a_i^2/8`  |
  |                    |                   |                        | +5a_i^2/8`        |                   |
  +--------------------+-------------------+------------------------+-------------------+-------------------+
  | **Para**           | :math:`a_c^2`     | :math:`a_i^2`          | :math:`3a_i^2/4`  | :math:`a_c^2      |
  |                    |                   |                        |                   | a_i^2/4`          |
  +--------------------+-------------------+------------------------+-------------------+-------------------+

  .. [#f1] Scattering lengths are related to bound cross sections by the surface are of a sphere. For example, if the coherent scattering length is :math:`a_c`, then the bound coherent scattering cross section is :math:`\sigma_{c}=4\pi a_c^2`. Furthermore, the total bound cross section :math:`\sigma_b=\sigma_c+\sigma_i` would be equal to :math:`4\pi(a_c^2+a_i^2)`.







.. .. code-block:: python
   :emphasize-lines: 3,5
   # user-provided values
   S(k)      = [ s0, s1, s2, ... ] # static structure factor S(k)
   kappaGrid = [ k0, k1, k2, ... ] # kappa grid that S(k) is on 
   for b in betas:
     for a in alphas:
       kappa    = k(a) # from alpha calculate wave number 
       S(kappa)        # interpolate on S(k) grid for the given kappa value
       reducedAlpha = a / S(kappa)
       S_coh = S(
       
       

