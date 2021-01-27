.. This is a comment. Note how any initial comments are moved by
   transforms to after the document title, subtitle, and docinfo.

.. demo.rst from: http://docutils.sourceforge.net/docs/user/rst/demo.txt

.. .. |EXAMPLE| image:: _images/temp.png
..    :width: 1em

------------------------------------
Multiple Temp. H in H2O 
------------------------------------

This is an example of H in H2O, which has oxygen as a secondary scatterer and involves multiple temperatures. The main purpose of this example is to illustrate how to process thermal scattering data for different temperatures, where each temperature is characterized using a different phonon distribution.

..
  COMMENT: .. contents:: Table of Contents
   :emphasize-lines: 1


-------------------------------------------------------------------------------


**Cards 1-2**

.. literalinclude:: exampleInputs/multipleTemps_H_H2O
   :language: html
   :lines: 1-3

Here, we use Card 1 to specify the output file (tape24), while Card 2 carries the title for the output file.


-------------------------------------------------------------------------------

**Card 3**

.. literalinclude:: exampleInputs/multipleTemps_H_H2O
   :language: html
   :lines: 1-4

Card 3 has three values - the first [NTEMPR] requests that scattering data be prepared for three temperatures, the second [IPRINT] indicates that a high verbosity be used in the output file, and the third value [IPHON] means that the phonon expansion sum should include 200 terms. 



-------------------------------------------------------------------------------

**Card 4**

.. literalinclude:: exampleInputs/multipleTemps_H_H2O
   :language: html
   :lines: 1-5

Card 4 sets some preliminary information for the calculation. The first value [MAT] is the identification tag for water, 1001 is the ZA value, calculated as 

  .. math::
    ZA = (1000.0*Z) + A.

The third and fourth values [ISABT and ILOG, respectively] indicate that the user that the final output scattering law should be symmetric [ISABT=0] and not in logarithmic form [ILOG=0].



-------------------------------------------------------------------------------

**Card 5**

.. literalinclude:: exampleInputs/multipleTemps_H_H2O
   :language: html
   :lines: 1-6

Card 5 contains information on the primary scatterer. The atomic weight ratio [AWR] is set to 0.9991 and the bound scattering cross section [SPR] is 20.436 b. 

The third value on Card 5 is the number of principal scatterers [NPR], which is set to two. This is because, of course, there are two hydrogen atoms per water molecule. 

The final three values on Card 5 are IEL, NCOLD, and NSK. IEL being set to zero indicates that no coherent elastic scattering calculation should be performed, NCOLD equal to zero means this is not a very cold Hydrogen calculation, and NSK means that there is no intermolecular coherence requested. 


-------------------------------------------------------------------------------

**Card 6**

.. literalinclude:: exampleInputs/multipleTemps_H_H2O
   :language: html
   :lines: 1-7

Card 6 deals with the secondary scatterer, if applicable. 

The first value on this card, NSS, being set to to 1 means that a secondary scatterer should be considered. If this value was set to zero, the rest of this card would not be necessary.

The following four inputs on Card 6 indicate the secondary scatterer type [B7], the atomic weight ratio for the secondary scatterer [AWS], the free cross section for the secondary scatterer [SPS], and the number of secondary-scattering atoms [MSS]. 


-------------------------------------------------------------------------------

**Card 7-9**

.. literalinclude:: exampleInputs/multipleTemps_H_H2O
   :language: html
   :lines: 1-15

The NALPHA input Card 7 states that 10 :math:`\alpha` values will be provided on Card 8. Similarly, NBETA on Card 7 states that 15 :math:`\beta` values will be give on Card 9.

The LAT input on Card 7 indicates that the :math:`\alpha` and :math:`\beta` values provided should be scaled by :math:`.0253/k_bT`, where :math:`k_bT` is the temperature in eV.

-------------------------------------------------------------------------------

**Card 10-16, T=293.6 K**

.. literalinclude:: exampleInputs/multipleTemps_H_H2O
   :language: html
   :lines: 1-34

Here, we begin the temperature loop. As stated in Card 3, there are three temperatures requested, and in this case, Cards 10-16 will be repeated for each temperature. 

Card 10 states the temperature. Cards 11 and 12 describe the solid-type contribution of the phonon distribution. DELTA is the spacing of the solid-type distribution, NI is the number of points that will be provided on Card 12, and Card 12 contains the actual solid-type distribution.

Card 13 contains information on the translational spectra - translational weight TWT, diffusion constant C, and solid-type weight TBETA. 

The only value on Card 14 is the number of discrete oscillators to be provided. Since this is set to a non-zero value, Cards 15 and 16 (which contain the oscillator energies and weights) must be provided. 



-------------------------------------------------------------------------------

**Card 10-16, T=500 K, T=600 K**

.. literalinclude:: exampleInputs/multipleTemps_H_H2O
   :language: html
   :lines: 1-74

Here we repeat Cards 10-16 again, for the second and third iterations of the temperature loop. These values can be the same or different values as those from the first temperature loop. Here, for instance, the solid-type distributions and translational components change from temperature to temperature, but the discrete oscillator energies and weights remain the same.



-------------------------------------------------------------------------------



**Card 20**

.. literalinclude:: exampleInputs/multipleTemps_H_H2O
   :language: html
   :lines: 1-

*Cards 17-19 are invoked when an inelastic coherent approximation is requested. Since no intermolecular coherence was requested (i.e. NSK on Card 5 is set to 0), these cards are omitted. Instead, we continue directly to card 20.*

Card 20 is a set of comments that will be included in the final output. These comments are read in until a blank line (consisting of only a "/") is read in.
