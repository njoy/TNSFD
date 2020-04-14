.. This is a comment. Note how any initial comments are moved by
   transforms to after the document title, subtitle, and docinfo.

.. demo.rst from: http://docutils.sourceforge.net/docs/user/rst/demo.txt

.. |EXAMPLE| image:: _images/temp.png
   :width: 1em

.. _theory:

**************************************
Theory of Thermal Neutron Scattering
**************************************

..
  COMMENT: .. contents:: Table of Contents






What are Thermal Neutrons?
===========================

LEAPR aims to describe the ways in which low energy neutrons (with energy on the order of 1 eV or less) interact with material. Accurately describing these interactions is crucial for adequate modeling of thermal nuclear systems. A neutron at room temperature has an energy of approximately 0.025 eV, meaning that its de Broglie wavelength is about 1 angstrom which is close to typical interatomic spacing in materials. This can complicate neutron-target interactions, and thus describing thermal scattering must account for the wave-like behavior of neutrons. 


.. _overview_types_of_scattering:

Types of Scattering
=========================

The probability of a neutron with initial energy and solid angle :math:`(E,\Omega)` scattering to have some final energy and solid angle :math:`(E',\Omega')` is described using the double differential scattering cross section :math:`\sigma(E\rightarrow E', \Omega\rightarrow\Omega')`. This cross section describes both elastic and inelastic scattering, both of which have a coherent and incoherent contribution.

.. image:: _images/scatteringBreakdown.jpeg

.. In elastic scattering, total kinetic energy (i.e. sum of neutron and target kinetic energy) is conserved, which is not the case for inelastic scattering. Inelastic scattering thus requires for some excitation of the target to occur, which accounts for the difference between initial and final kinetic energy. 


Elastic vs. Inelastic 
---------------------------------
Elastic scattering means that the total kinetic energy of the system (neutron plus target) is the same before and after the scattering collision. This is contrasted with inelastic scattering, where kinetic energy is not conserved. This change in energy is due to some excitation (or de-excitation) occurred. 

----------------------------------------------------------------------------

**Does an elastically scattered neutron have the same incoming/outgoing energy?**

If a neutron scatters off of a target of similar size (e.g. a hydrogen nucleus), the neutron can lose nearly all its energy. If the target is significantly more massive than the neutron, however, conservation of momentum prevents the neutron from losing a large amount of its energy. 

When fast / resonance range neutrons scatter off of media, their incoming energy is so much larger than the molecular bonds of the scattering material, which allows the neutron to effectively "see" the target as just a free atom. Thermal neutrons, however, do not have enough incoming energy to allow them to ignore molecular and lattice bonds. They thus cannot scatter off of a free atom, but rather scatter off of an atom that is part of a much larger aggregate system. This can make it harder for the neutron to lose a large fraction of its energy in an elastic scattering event. 

The incoming and outgoing energies of scattered thermal neutrons are not the same, but will have a tendency to be much closer than those of higher energy neutrons. 

----------------------------------------------------------------------------

**Isn't inelastic scattering a threshold reaction?**

For high energy neutrons, the excitation associated with an inelastic collision is a *nuclear* excitation, where the target nucleus is brought to some excited state. This requires a significant amount of energy, and thus nuclear inelastic scattering is a *threshold* reaction, as seen below.

.. figure:: _images/U238_xs.png
    :width: 60%
    :align: center

    Elastic and nuclear inelastic scattering cross sections for U-238 (from NNDC). Note that nuclear inelastic scattering is a threshold reaction that does not appreciable contribute until incoming neutrons have an incoming energy of about 0.1 MeV.


For thermal (low energy) neutrons, inelastic scattering is caused by some *molecular* or *lattice* excitation, where vibrational modes of a multi-atom system are excited. Molecular excitations can be induced by neutrons with energy on the order of 1 eV and do not exhibit the same extreme threshold behavior as does nuclear excitations. Thermal inelastic scattering is thus focused on molecular excitations. The availability of vibrational modes that could be excited in some lattice system is described by the vibrational frequency spectrum / phonon density of states / phonon frequency distribution. 

.. .. math::
  \sigma(E\rightarrow E',\Omega\rightarrow\Omega') = \sigma_{coh}(E\rightarrow E',\Omega\rightarrow\Omega') + \sigma_{inc}(E\rightarrow E,\Omega\rightarrow\Omega') 




Coherent vs. Incoherent 
--------------------------

Neutron scattering is the interaction of wavefunctions, where the incoming neuton wave interacts with a target and creates a scattered spherical wave. This is simply due to the fact that a large incoming wave hitting a (relatively) small target will result in a spherical scattered wave. Additionally, large thermal neutron wavelength means that the neutron can exist atop multiple atoms at once, creating simultaneous scattering sites. 

When these scattered spherical waves, which originate from different scattering sites interfere, they can do so either coherently (meaning periodic constructive growth or destructive cancellation) or incoherently (meaning that no large-scale periodic growth or cancellation occurs). 

Incoherent scattering is significantly easier to model, and LEAPR has the ability to desribe both elastic and inelastic incoherent scattering (which correspond to total kinetic energy conservation and change, respectively). Coherent scattering is harder to quantify, and LEAPR currently has the ability to describe only elastic coherent scattering for selected materials. 

For reactor systems, incoherent scattering primarily dominates (which facilitates data preparation, as incoherent scattering is simpler to process). There are some instances, however, where neglecting coherent scattering could result in significant error. For a brief discussion detailing *when* coherent scattering is important, please see [SOURCE].

Overview of Objectives
--------------------------
As seen above, there are multiple types of thermal scattering that occur in a reactor system. LEAPR aims to prepare data describing these different types of interactions, namely the **scattering law**, :math:`S(\alpha,\beta)`. The scattering law is a function of dimensionless momentum and energy exchange (:math:`\alpha` and :math:`\beta`, respectively), 

.. math:: 
  \alpha = \frac{E'+E-2\mu\sqrt{EE'}}{Ak_bT}\qquad~\qquad\beta=\frac{E'-E}{k_bT}.

Once obtained, the scattering law can be used to calculate the double differential scattering cross section,

.. math::
  \frac{d^2\sigma}{dE'~d\Omega }=\frac{\sigma_b}{2k_bT}\sqrt{\frac{E'}{E}}S(\alpha,\beta)

.. [IS THIS IN THE INCOHERENT APPROXIMATION I THINK SO BUT I"M NOT SURE CHECK YOUR BOOK]

Thus, the goal of LEAPR is to calculate this scattering law for some user-provided :math:`\alpha,\beta` grid. Doing so requires many approximation that will be described in the coming sections. Incoherent scattering is significantly easier to describe, and LEAPR calculates this contribution to the scattering law by use of a user-provided vibrational frequency spectrum (sometimes known as frequency distribution, phonon distribution, phonon density of states, etc.). Cohernt scattering is significantly more difficult to describe, and so LEAPR's ability to calculate coherent scattering contributions is much more limited. Coherent elastic scattering capabilities are available for certain materials, and coherent inelastic scattering can be approximated if additional material data (namely, the static structure factor) is provided.





.. _theory_incoherent:

Incoherent Scattering (Elastic and Inelastic)
==============================================
LEAPR describes incoherent scattering by starting with a continuous (solid-type) distribution and considering additional feautres (e.g. the existence of very sharp peaks or diffusive behavior) if necessary. The continuous calculation *must always be performed*, and additional features that can also be considered include the existence of discrete oscillators (Einstein oscillators), translative/diffusive behavior, cold Hydrogen/Deuterium, and intermolecular interference. 

The continuous calculation will now be discussed, followed by each of the aforementioned features.


.. _theory_incoherent_contin: 

Continuous Treatment 
-------------------------

To calculate the incoherent contribution to the scattering law, the following equations must be solved,

.. math::
    S^{(s)}_{n.sym}(\alpha, \beta)=\frac{1}{2 \pi} \int_{-\infty}^{\infty} \mathrm{e}^{i \beta t} \mathrm{e}^{-\gamma(t)} d t
..   :label: continuousSAB

.. math::
    \gamma(t)=\alpha\lambda_s -\alpha \int_{-\infty}^\infty P(\beta')~\mathrm{e}^{-\beta'/2}~\mathrm{e}^{-i\beta' t}~d\beta'
..    :label: gammaDefinition

.. math:: 
  P(\beta)=\frac{\rho(\beta)}{2\beta\sinh(\beta/2)},
..  :label: PDefinition

where :math:`S^{(s)}_{n.sym}` is the non-symmetric scattering law for solids, :math:`\rho(\beta)` is the phonon frequency distribution, and :math:`\lambda_s` is the Debye-Waller coefficient. 
.. For a introductory discussion on the phonon frequency spectrum, please see :ref:`background_phonon_dos`. 

By Taylor expanding :math:`\gamma(t)`, the above can be simplified to 

.. .. math:: 
    S^{(s)}_{n.sym}(\alpha,\beta) = \mathrm{e}^{-\alpha\lambda_s}\sum_{n=0}^\infty \frac{\alpha^n}{n!} W_n(\beta)

.. math:: 
    S^{(s)}_{n.sym}(\alpha,\beta) = \mathrm{e}^{-\alpha\lambda_s}\sum_{n=0}^\infty \frac{\alpha^n\lambda_s^n}{n!} \mathcal{T}_n(\beta)


where


.. math:: 
    \mathcal{T}_1(\beta) = \frac{1}{\lambda_s}P(\beta)~\mathrm{e}^{-\beta/2}\qquad\mbox{and}\qquad \mathcal{T}_n(\beta) = \int_{-\infty}^\infty \mathcal{T}_1(\beta')~\mathcal{T}_{n-1}(\beta-\beta')~d\beta'.


.. .. math:: 
    W_1(\beta) = P(\beta)~\mathrm{e}^{-\beta/2}\qquad\mbox{and}\qquad W_n(\beta) = \int_{-\infty}^\infty W_1(\beta')~W_{n-1}(\beta-\beta')~d\beta'.


.. warning::
  **What approximations are made?**
  In describing the scattering behavior with a continuous, solid-type spectrum, a number of approximations are made, which are summarized below.

  +------------------+--------------------------------------------+-----------------------------------+
  | Approximation    | Description                                | Comments                          |
  |                  |                                            |                                   |
  +==================+============================================+===================================+
  | | Gaussian       | | In the definition of                     | | See Parks [REFERENCE] for more  | 
  | | approximation  |   :math:`S(\alpha,\beta)`,                 | | discussion. Not typically       |
  |                  | | :math:`\mathrm{exp}\Big(-\alpha\gamma(t) | | considered a significant source |
  |                  |   +\alpha^2\gamma_2(t)+\dots\Big)`         | | of error                        |
  |                  | | is approximated as :math:`\mathrm{exp}   |                                   | 
  |                  |   \big(-\alpha\gamma(t)\big)`.             |                                   | 
  +------------------+--------------------------------------------+-----------------------------------+
  | | Incoherent     | | While this is not an approximation made  | | This is typically valid practice|
  | | approximation  | | in the above equations, it is important  | | for materials with either low   |
  |                  | | to note that LEAPR uses the incoherent   | | coherent cross sections or      |
  |                  | | equations to desribe both coherent and   | | randomly-oriented crystallites. |
  |                  | | incoherent scattering.                   |                                   |
  +------------------+--------------------------------------------+-----------------------------------+
  | | Validity of    | | The continuous calculation requires an   | | Before using a published phonon |
  | | phonon DOS     | | an input phonon spectrum, which are      | | spectrum, ensure that it        |
  |                  | | specific to material composition,        | | corresponds to the correct      |
  |                  | | crystalline structure, and temperature.  | | material, structure, and temp.  |
  +------------------+--------------------------------------------+-----------------------------------+
  | | Randomly       | | In order to separate scattering into     | | Spin-correlation is important   |
  | | oriented spins | | coherent and incoherent components,      | | while considering materials like|
  |                  | | spin-correlation effects are ignored.    | | liquid hydrogen/deuterium, which|
  |                  | |                                          | | are considered separately later.|
  +------------------+--------------------------------------------+-----------------------------------+
  | | Edge effects   | | Edge effects are not considered, meaning | | Ignoring edge effects is a      |
  | | are ignored    | | that the scatterer is considered to be   | | standard approximations that is | 
  |                  | | infinitely large.                        | | is not typically considered to  |
  |                  |                                            | | cause significant error.        |
  +------------------+--------------------------------------------+-----------------------------------+
  | | Atoms of only  | | Atoms of only one kind are considered.   | | In a material like              |
  | | one kind are   | | Treatment for mixed moderators  will be  |   :math:`\mbox{H}_2\mbox{O}`,     | 
  | | present        | | discussed later.                         | | scattering from hydrogen is     |
  |                  |                                            | | significantly more important    |
  |                  |                                            | | than that from oxygen, so       |
  |                  |                                            | | that only hydrogen exists is a  |
  |                  |                                            | | valid simplification. This is   |
  |                  |                                            | | not the case for materials like |
  |                  |                                            | | beryllium oxide, however.       | 
  +------------------+--------------------------------------------+-----------------------------------+
  | | Simplified     | | Atoms are assumed to be bound  by        | | This approach is applied to     | 
  | | crystal        | | isotropic, harmonic forces in a crystal  | | many materials that do not      |
  | | structure      | | with cubic symmetry and one atom per     | | display these characteristics,  |
  |                  | | unit cell.                               | | and is believed to be an        |
  |                  |                                            | | adequate approximation.         |
  +------------------+--------------------------------------------+-----------------------------------+

.. seealso::
  **Want more information?**

  +-------------------+-----------------------------------------------------------------------------------+
  | Topic             | Resources                                                                         |
  +===================+===================================================================================+
  | | Phonon frequency| | Please see :ref:`background_phonon_dos`                                         |
  | | spectrum theory | |                                                                                 |
  +-------------------+-----------------------------------------------------------------------------------+
  | | Phonon frequency| | 1. http://materialsproject.com/                                                 |
  | | spectrum        | | 2. ENDF-B/VIII release available at https://www.nndc.bnl.gov/endf/b8.0/         |
  | | availability    | |    has a thermal neutron scattering sublibrary, with ENDF outputs and the       |
  |                   | |    LEAPR inputs with which the ENDF files were generated. In those LEAPR inputs |
  |                   | |    are phonon distributions.                                                    |
  +-------------------+-----------------------------------------------------------------------------------+
  | | Derivation of   | | Please see :ref:`additional_phonon_expansion`                                   |
  | | Phonon Expansion|                                                                                   |
  +-------------------+-----------------------------------------------------------------------------------+
  | |                 |                                                                                   |
  +-------------------+-----------------------------------------------------------------------------------+

..  | | Debye-Waller    | | please see [  ]                                                                 |
  | | coefficient     | |                                                                                 |
  +-------------------+-----------------------------------------------------------------------------------+







Translational Behavior
--------------------------------------
Thermal neutron scattering off of liquids can be described by solving a solid-type spectrum that is combined with a diffusive term. A popular diffusive model is the "Effective Width Model", which is defined as 

.. math:: 
  S_{n.sym}^{(t)}(\alpha,\beta) = \frac{2c\omega_t\alpha}{\pi}~\mathrm{exp}\left({2c^2\omega_t\alpha-\beta/2}\right)\sqrt{\frac{c^2+0.25}{\beta^2+4c^2\omega_t^2\alpha^2}}\mathrm{K}_1\left[\sqrt{c^2+0.25}\sqrt{\beta^2+4c^2\omega_t^2\alpha^2}\right]

with a corresponding frequency spectrum

.. math::
  \rho(\beta)=\omega_t\frac{4c}{\pi\beta}\sqrt{c^2+0.25}~\sinh(\beta/2)~\mbox{K}_1\left[\sqrt{c^2+0.25}~\beta\right]

where :math:`K_n(x)` is the modified Bessel function of the second kind with order :math:`n`.


An alternative to the effective width model is the free gas model, which is defined as 

.. math:: 
  S^{(f)}_{n.sym}(\alpha,\beta) = \frac{1}{\sqrt{4\pi\omega_t\alpha}}~\mathrm{exp}\left[-\frac{(\omega_t\alpha+\beta)^2}{4\omega_t\alpha}\right]


So to model a diffusive material, the solid-type solution obtained from the vibrational spectrum is convolved with some appropriate translative model (i.e. effective width model or free gas model). 













.. _theory_incoherent_discre: 

Discrete Oscillators
-------------------------
The blue region in the below figure shows the vibrational frequency spectrum for hydrogen bound in water [inspired by [CITE DAMIAN]]. Note the two prominent peaks near 0.20 eV and 0.42 eV. If a user wanted to process scattering data for this material, they could provide this full spectrum to LEAPR and have it run the full continuous calculation.

.. figure:: _images/waterPhononDOS_hatch.png
    :width: 90%
    :align: center

    The vibrational frequency spectrum for H bound in water is shown above. 

Alternatively, LEAPR allows for users to represent these higher energy peaks as discrete oscillators, also known as "Einstein oscillators". These oscilltors are represented as weighted Dirac-:math:`\delta` functions in the frequency distribution, which brings the blue distribution in the above figure to become the red distribution. The lower energy, continuous distribution is still the same, but the two higher energy peaks are replaced with weighted :math:`\delta` functions (the weighting is not represented in the above figure).

As can be seen in the figure above, reducing the peaks to simple oscillators eliminates peak resolution and is **only recommended for validating and replicating existing data**. 

The scattering law contribution from a discrete oscillator is

.. math:: 
  S^{(i)}_{n.sym}(\alpha,\beta)=\mathrm{e}^{-\alpha\lambda_i}\sum_{n=-\infty}^\infty\delta(\beta-n\beta_i)~I_n\left[\frac{\alpha\omega_i}{\beta_i\sinh(\beta_i/2)}\right]~\mathrm{e}^{-n\beta_i/2}

which is a direct simplification of the scattering law from the continuous case (defined in Eq. [  ]).

To process the scattering law for a material described by discrete oscillators, the discrete ocsillator contribution :math:`S^{(i)}_{n.sym}(\alpha,\beta)` is calcululated for each :math:`i^{th}` oscillator. These individual contributions are convolved with the solid-type contribution :math:`S_{n.sym}^{(s)}(\alpha,\beta)` which, in the figure above corresponds with the lower-energy part of the red distribution.

.. warning::
  **What approximations are made?**
  The discrete oscillator formulation is a simplification of the continuous treatment, and thus adopts those along with additional approximations. Only the additional approximations are presented here. 

  +-------------------+----------------------------------------------+-----------------------------------+
  | Approximation     | Description                                  | Comments                          |
  |                   |                                              |                                   |
  +===================+==============================================+===================================+
  | | Einstein        | | The discrete oscillator approximation      | | See Parks [REFERENCE] for more  | 
  | | crystal approx. | | is the analytic solution for the           | | discussion. This has historical |
  |                   | | scattering law, when considering a         | | significance but is not         |
  |                   | | perfect cubic structure of atoms that      | | recommended for modern problems | 
  |                   | | all vibrate with the same frequency,       |                                   | 
  |                   | | thus meaning that any invoked vibrational  |                                   |
  |                   | | frequencies must be multiples of some      |                                   |
  |                   |   :math:`\omega`.                            |                                   | 
  +-------------------+----------------------------------------------+-----------------------------------+


.. seealso::
  **Want more information?**

  +-----------------------+---------------------------------------------------------------------------------+
  | Topic                 | Resources                                                                       |
  +=======================+=================================================================================+
  | | Equivalence between | | Please see :ref:`additional_discrete_oscillator`                              |  
  | | discrete oscillator | |                                                                               |
  | | and continuous      | |                                                                               |
  | | treatment           | |                                                                               | 
  +-----------------------+---------------------------------------------------------------------------------+
..  | | Experimental support| | Please see [  ] this will show how we                                         |
  | | for validity of the | | got to the phonon expansion                                                   |
  | | discrete oscillator | |                                                                               |
  | | treatment           | |                                                                               |
  +-----------------------+---------------------------------------------------------------------------------+







Coherent Scattering (Elastic)
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






Coherent Scattering (Inelastic) Approximations
================================================

Skold and Vineyard
------------------------

The incoherent approximation, which is made while using the continuous, translational, and discrete oscillator methods, ignores coherent effects. There are some material, however, in which scattered neutron waves can interfere with each other in meaningful ways. This inter-molecular coherence occurs when there is both a significant bound coherent scattering cross section (property of the atoms) as well as some correlation between the positions of nearby molecules (property of the lattice). If these requirements are met, coherent scattering may become non-negligible, at which point its effect can be accounted for by using the **Vineyard** or **Skold** approximations. 

In these methods, the scattering law is separated into a coherent and an incoherent contribution, which are weighted using a *coherent fraction* :math:`c`. The incoherent contribution to the scattering law can be obtained using the aforementioned methods (continuous, discrete, and translational), but the coherent contribution must be approximated.

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
The continuous treatment equations introduced in :ref:`theory_incoherent_contin` were stated assuming that spins are randomly distributed. This approximation is valid for most materials, but breaks down when describing liquid hydrogen and deuterium. To correct this error, quantum mechanical treatment is required to account for spin-spin correlations for atoms in the same molecule/structure.

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
       
       



Special Cases and Misc. Functions
==============================================

Short-collision time approximation 
------------------------------------
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


