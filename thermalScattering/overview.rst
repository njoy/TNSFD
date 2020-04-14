.. This is a comment. Note how any initial comments are moved by
   transforms to after the document title, subtitle, and docinfo.

.. demo.rst from: http://docutils.sourceforge.net/docs/user/rst/demo.txt

.. |EXAMPLE| image:: _images/temp.png
   :width: 1em

.. _theory:

**************************************
Overview of Thermal Neutron Scattering
**************************************

..
  COMMENT: .. contents:: Table of Contents


What are Thermal Neutrons?
===========================

Molecular bonds are typically on the order of a few eV, so for neutrons above this threshold, molecular structure will not significantly affect the scattering behavior. Thermal neutrons, which are neutrons that lie below this threshold, cannot consider a target atom in isolation but rather must consider the entire structure. 

Two interesting phenomena come into play for thermal neutrons:

 * **Neutron-phonon interactions**

   Since thermal neutrons cannot break molecular bonds between atoms, they must interact with the larger, aggregate structure, which at finite temperatures has vibrational excitations. These vibrational modes, also known as phonons, can interact with thermal neutron scattering to create inelastic collisions. 

  If a thermal neutron collides off of a material, it has the possibility to create or destroy one or more phonons. If a neutron with incoming energy :math:`E_{in}` creates a phonon with energy :math:`E_{ph}`, the neutron's outgoing energy is :math:`E_{out}=E_{in}-E_{ph}`. Similarly, if the neutron were to destroy said phonon, its outgoing energy would be :math:`E_{out}=E_{in}+E_{ph}`.

  Thermal neutrons can interact with many phonons of different energies, and the distribution of possible phonons that could exist in a material is represented in that material's phonon density of states.


 * **de Broglie wavelength**

  Thermal neutrons have a de Broglie wavelength that is on the order of 1 Angstrom, similar to typicaly interatomic spacings in solids. This means that a neutron may simulaneously interact with multiple atoms in the material, further complicating thermal scattering and forcing us to depart from classical intuition that may otherwise apply.


For more information regarding phonons and the importance of the phonon distribution in thermal neutron scattering, please see :ref:`Vibrational (Phonon) Denstiy of States<background_phonon_dos>`

.. For neutrons above 1-10 eV, neutron scattering cross sections are functions of nuclide type, material temperature, and neutron energy. 
.. Molecular bonds are on the order of a few eV, so neutrons above about 10 eV are not strongly affected by material structure and their cross sections are simply a function of nuclide and neutron energy. For neutrons below 1-10 eV, material structure can also strongly affect scattering behavior. Slow neutrons have energies on the order of a materials vibrational modes, thus a scattering event could be strongly influenced by the creation or destruction of these normal modes (also known as phonons).


.. LEAPR aims to describe the ways in which low energy neutrons (with energy on the order of 1 eV or less) interact with material. Accurately describing these interactions is crucial for adequate modeling of thermal nuclear systems. A neutron at room temperature has an energy of approximately 0.025 eV, meaning that its de Broglie wavelength is about 1 angstrom which is close to typical interatomic spacing in materials. This can complicate neutron-target interactions, and thus describing thermal scattering must account for the wave-like behavior of neutrons. 


.. _overview_types_of_scattering:

Types of Scattering
=========================


The double differential scattering cross section for thermal neutrons is comprised of a coherent component and an incoherent component,
.. The probability of a neutron with initial energy and solid angle scattering to have some final energy and solid angle :math:`(E',\Omega')` is described using the double differential scattering cross section :math:`\sigma(E\rightarrow E', \Omega\rightarrow\Omega')`. The scattering cross section has a coherent and an incoherent component, 

.. math::
  \sigma(E\rightarrow E',\Omega\rightarrow\Omega') = \sigma_{inc}(E\rightarrow E',\Omega\rightarrow\Omega') + \sigma_{coh}(E\rightarrow E',\Omega\rightarrow\Omega').


Coherent vs Incoherent Scattering
------------------------------------------------------------------
Neutron scattering is the interaction of wavefunctions, where the incoming neuton wave interacts with a target and creates a scattered spherical wave. This is simply due to the fact that a large incoming wave hitting a (relatively) small target will result in a spherical scattered wave. Additionally, large thermal neutron wavelength means that the neutron can exist atop multiple atoms at once, creating simultaneous scattering sites. 

When these scattered spherical waves, which originate from different scattering sites interfere, they can do so either coherently (meaning periodic constructive growth or destructive cancellation) or incoherently (meaning that no large-scale periodic growth or cancellation occurs). 

The coherent and incoherent scattering contributions have the following forms, 

.. math::
  \sigma_{inc}(E\rightarrow E',\Omega\rightarrow\Omega') = \frac{\sigma_{inc}}{4\pi\hbar}\sqrt{\frac{E'}{E}}\frac{1}{2\pi}\int_{-\infty}^\infty \int \mathrm{e}^{\epsilon t/\hbar-\mathbf{k}\mathbf{r}}~G_s(\mathbf{r},t)~d\mathbf{r}~dt

  \sigma_{coh}(E\rightarrow E',\Omega\rightarrow\Omega') = \frac{\sigma_{coh}}{4\pi\hbar}\sqrt{\frac{E'}{E}}\frac{1}{2\pi}\int_{-\infty}^\infty \int \mathrm{e}^{\epsilon t/\hbar-\mathbf{k}\mathbf{r}}~G(\mathbf{r},t)~d\mathbf{r}~dt

where the above integrals are only dependent on changes of neutron energy :math:`\epsilon=E'-E` and changes of neutron momentum :math:`\hbar\mathbf{k}=m(\mathbf{v'}-\mathbf{v})`, rather than than absolute energy and momentum. The :math:`G(\mathbf{r},t)` function that appears in the coherent contribution is the **pair distribution function**, which has a "self" component :math:`G_s` which appears in the incoherent constribution and a "distinct" component :math:`G_d`.

.. math::
  G(\mathbf{r},t)=G_s(\mathbf{r},t)+G_d(\mathbf{r},t)

Speaking loosely, if there exists a particle at the origin at time :math:`t=0`, then :math:`G(\mathbf{r},t)` is the probability that a particle 


   



This cross section describes both elastic and inelastic scattering, both of which have a coherent and incoherent contribution.

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

