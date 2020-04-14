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

Vibrational (Phonon) Density of States
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



