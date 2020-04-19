.. This is a comment. Note how any initial comments are moved by
   transforms to after the document title, subtitle, and docinfo.

.. demo.rst from: http://docutils.sourceforge.net/docs/user/rst/demo.txt

.. |EXAMPLE| image:: _images/temp.png
   :width: 1em

.. _general_theory:

**************************************
Overview of Thermal Neutron Scattering
**************************************

..
  COMMENT: .. contents:: Table of Contents


What are Thermal Neutrons?
===========================

Molecular bonds are typically on the order of a few eV, so for neutrons above this threshold, molecular structure will not significantly affect the scattering behavior. Thermal neutrons, which lie below this threshold, cannot consider a target atom in isolation but rather must consider the entire structure. 

Two interesting phenomena come into play for thermal neutrons:


 * **de Broglie wavelength**

  Thermal neutrons have a de Broglie wavelength that is on the order of 1 Angstrom, similar to typical interatomic spacings in solids. This means that a neutron may simulaneously interact with multiple atoms in the material, further complicating thermal scattering and forcing us to depart from classical intuition that may otherwise apply.


 * **Neutron-phonon interactions**

   Since thermal neutrons cannot break molecular bonds between atoms, they must interact with the larger, aggregate structure, which at finite temperatures has vibrational excitations. These vibrational modes, also known as phonons, can interact with thermal neutron scattering to create inelastic collisions. 

  If a thermal neutron collides off of a material, it has the possibility to create or destroy one or more phonons. If a neutron with incoming energy :math:`E_{in}` creates a phonon with energy :math:`E_{ph}`, the neutron's outgoing energy is :math:`E_{out}=E_{in}-E_{ph}`. Similarly, if the neutron were to destroy said phonon, its outgoing energy would be :math:`E_{out}=E_{in}+E_{ph}`.

  Thermal neutrons can interact with many phonons of different energies, and the distribution of possible phonons that could exist in a material is represented in that material's phonon density of states.


  Since thermal neutrons do not have sufficient energy to knock an atom from the material, any data prepared for a atom has to account for the material it belongs to. Thermal neutron scattering data must be prepared for "hydrogen in water", for example, instead of just for "hydrogen" in general.




For more information regarding phonons and the importance of the phonon distribution in thermal neutron scattering, please see :ref:`Vibrational (Phonon) Denstiy of States<background_phonon_dos>`

.. For neutrons above 1-10 eV, neutron scattering cross sections are functions of nuclide type, material temperature, and neutron energy. 
.. Molecular bonds are on the order of a few eV, so neutrons above about 10 eV are not strongly affected by material structure and their cross sections are simply a function of nuclide and neutron energy. For neutrons below 1-10 eV, material structure can also strongly affect scattering behavior. Slow neutrons have energies on the order of a materials vibrational modes, thus a scattering event could be strongly influenced by the creation or destruction of these normal modes (also known as phonons).


.. LEAPR aims to describe the ways in which low energy neutrons (with energy on the order of 1 eV or less) interact with material. Accurately describing these interactions is crucial for adequate modeling of thermal nuclear systems. A neutron at room temperature has an energy of approximately 0.025 eV, meaning that its de Broglie wavelength is about 1 angstrom which is close to typical interatomic spacing in materials. This can complicate neutron-target interactions, and thus describing thermal scattering must account for the wave-like behavior of neutrons. 


