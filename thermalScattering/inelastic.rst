
.. This is a comment. Note how any initial comments are moved by
   transforms to after the document title, subtitle, and docinfo.

.. demo.rst from: http://docutils.sourceforge.net/docs/user/rst/demo.txt

.. |EXAMPLE| image:: _images/temp.png
   :width: 1em

.. _inelastic_theory:

***************************************
Inelastic (Incoherent Approximation) 
***************************************

..
  COMMENT: .. contents:: Table of Contents

As introduced in :ref:`scatteringLaw`, the thermal neutron scattering cross section is 

.. math::
    \sigma(E\rightarrow E',\mu) = \frac{\sigma_b}{k_bT}\sqrt{\frac{E'}{E}}~S(\alpha,\beta). 

The two steps to preparing cross sections are:

1. Calculate the scattering law :math:`S(\alpha,\beta)`. This is primarily done by the LEAPR module.
2. Use the scattering law to calculate the cross section, and prepare the final data on ENDF files. This is performed by the THERMR module.
 
For more information on these steps, please see !!!!!!


Currently, the inelastic thermal neutron scattering uses the following approximations:



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
  | | Derivation of   | | Please see !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!                                   |
  | | Phonon Expansion|                                                                                   |
  +-------------------+-----------------------------------------------------------------------------------+
  | |                 |                                                                                   |
  +-------------------+-----------------------------------------------------------------------------------+

..  | | Debye-Waller    | | please see [  ]                                                                 |
  | | coefficient     | |                                                                                 |
  +-------------------+-----------------------------------------------------------------------------------+







