.. This is a comment. Note how any initial comments are moved by
   transforms to after the document title, subtitle, and docinfo.

.. demo.rst from: http://docutils.sourceforge.net/docs/user/rst/demo.txt

.. .. |EXAMPLE| image:: _images/temp.png
..    :width: 1em

------------------------------------------
Fe-026 (Single Temperature)
------------------------------------------



This example serves as a simplified input that would allow a user to prepare the thermal scattering law :math:`S(\alpha,\beta)` for describing Fe-56 at a single temperature. The example below uses very coarse :math:`\alpha` and :math:`\beta` grids, that should not be used for actual data preparation.

Note that parentheses following the forward slash will indicate the card number.

..
  COMMENT: .. contents:: Table of Contents
   :emphasize-lines: 1


-------------------------------------------------------------------------------


**Cards 1-2**

.. literalinclude:: exampleInputs/fe_singleTemp
   :language: html
   :lines: 1-3

- The first line defines the module, which is LEAPR. 
- Typically, the first card is used to specify input and output files, however since LEAPR does not read in any auxiliary files, only the output file need be specified. In this example, the output file will be located in the (unless otherwise specified) bin directory as "tape25".
- The second line (card 2) contains the descriptive title that will be used in the LEAPR output. 

.. -------------------------------------------------------------------------------

.. .. literalinclude:: exampleInputs/fe_singleTemp
..    :language: html
..    :lineno-start: 0
..    :lines: 1-3


-------------------------------------------------------------------------------

**Card 3**

.. literalinclude:: exampleInputs/fe_singleTemp
   :language: html
   :lines: 1-4

- The first value on Card 3 is the number of temperatures desired, which here is set to 1.
- In addition to the output file (for us, tape24), NJOY also returns a summary output file, which is traditionally labeled "output". Acceptable values are (0,1,2) where here we use 2 to indicate maximum verbosity. 
- Any LEAPR run will perform a phonon expansion calculation to represent the inelastic scattering behavior. The third input on Card 3 is the phonon expansion number, which indicates the number of terms :math:`N` that should be computed when approximating the sum in :ref:`the phonon expansion method<continuous_solid_type>`.

  This phonon expansion number is not specified on Card 3 here, and thus left to the default value of 100.

.. math:: 
  S^{(s)}_{n.sym}(\alpha,\beta) \approx \mathrm{e}^{-\alpha\lambda_s}\sum_{n=0}^N \frac{\alpha^n}{n!} W_n(\beta)


  

-------------------------------------------------------------------------------

**Card 4**

.. literalinclude:: exampleInputs/fe_singleTemp
   :language: html
   :lines: 1-5

- The first value on Card 4 is the MAT number (material identification number), and dictates what numerical tag will be on the output tape. Users are encouraged to use ENDF-specified values, when available [https://oecd-nea.org/dbdata/data/manual-endf/endf102.pdf].


- The second input is the :math:`ZA` value. For the case of Fe-56this is equal to 26056 as can be seen by the following rules:

    For isotopes, :math:`ZA` is equal to :math:`1000\,Z+A` where :math:`Z` and :math:`A` are the charge number and mass number. If the material is an element that has more than one naturally occurring isotope, then :math:`ZA` is equal to :math:`1000\,Z`. If the material is a compound, then :math:`ZA` is equal to :math:`ZA=\mbox{MAT}+100`.



- The third input on Card 4 is a flag for whether the output scattering law should be :ref:`symmetric or non-symmetric<symmetricNonsymmetric>`. By omitting this in our Card 4 line, we resort to the default value which is 0 (symmetric). 

- The fourth entry on card 4 is a flag for whether the output file should contain :math:`S(\alpha,\beta)` or :math:`\mbox{log}_{10}\big[S(\alpha,\beta)\big]` (which correspond to an entry value of 0 or 1, respectively). Writing results in log form is a standard ENDF approach of handling very small numbers for thermal scattering. Again, by omission we accep the default value of 0.

- The last entry on card 4 is the minimum value of :math:`S(\alpha,\beta)` to store. Here we use its default value of :math:`1\times10^{-75}`.



-------------------------------------------------------------------------------

**Card 5**

.. literalinclude:: exampleInputs/fe_singleTemp
   :language: html
   :lines: 1-6

LEAPR allows for either 1 or 2 scattering species to be considered in the same run. Card 5 is focused on the materials primary scatterer. If there is a secondary scatterer considered, that will be specified on the following card.  

- We first specify the atomic weight ratio of the primary scatterer (AWR), which is defined as the ratio of the mass of the material to that of the neutron. For Fe-56, we set this as 55.454. 

- The free atom scattering cross section :math:`\sigma_b` is set to 12.05. 
  .. These values can be obtained at https://www.nndc.bnl.gov/sigma under "resonance parameters - interpreted". 

- The number of primary scattering atoms. For hydrogen in water, this would be 2, and for Fe-56 we set this to 1.

- The fourth value is a flag for coherent elastic scattering (Bragg edges). A value of 6 is chosen which indicates iron.

- The fifth value is a cold hydrogen/deuterium flag, which dictates whether or not nuclear spins can be assumed to be distributed randomly. In most cases, this flag will be 0, indicating that spins are randomly distributed (i.e. the material is not cold hydrogen or cold deuterium).

- The final value defines whether intermolecular coherence will be accounted for, and if so, how it will be approximated. Here, we are not concerned with this effect and leave the flag set to its default valoue of 0.


-------------------------------------------------------------------------------

**Card 6**

.. literalinclude:: exampleInputs/fe_singleTemp
   :language: html
   :lines: 1-7


Card 5 is focused on the materials primary scatterer. If there is a secondary scatterer considered, that will be specified on Card 6. 

The first value of Card 6 is the number of secondary scatterers, which for this Fe-56 calculation is set to 0. The rest of the values on Card 6 need not be specified.





-------------------------------------------------------------------------------

**Card 7-9**

.. literalinclude:: exampleInputs/fe_singleTemp
   :language: html
   :lines: 1-13

Now that general information on the material and calculation have been provided, we now move to define the :math:`\alpha` and :math:`\beta` grids desired for this run. 

- Card 7 defines the number of :math:`\alpha` values (8), the number of :math:`\beta` values (7) and whether the :math:`\alpha,\beta` grids should be scaled. If the scaling option is set to 0, neither grid is scaled. Since it is set to 1, however, both grids will be scaled by :math:`0.0253/k_bT` where :math:`k_bT` is the temperature in eV. 

- Card 8 provides the :math:`\alpha` values, and Card 9 provides the :math:`\beta` values. For lines with many values of inputs, such as Cards 8 and 9 here, the input values can span multiple lines since LEAPR was already informed of the number of :math:`\alpha` and :math:`\beta` values to expect in Card 7.


Note that, as seen above, a blank line can be added between lines of LEAPR input to separate cards. 

-------------------------------------------------------------------------------

**Card 10-13**

.. literalinclude:: exampleInputs/fe_singleTemp
   :language: html
   :lines: 1-31

- Card 10 provides the desired temperature in K.

- Cards 11 and 12 define the vibrational frequency spectrum (phonon distribution, phonon density of states, etc.) that will be used in the continuous, phonon expansion calculation. The frequency distribution is provided on a uniformly spaced energy grid (energy grid has units of eV). 

  - The first entry of Card 11 is the energy spacing on this grid, and the second entry is the number of values in this frequency distribution. 

  - Card 12 provides the frequency distribution values. Note that the first and last values should be 0.0. The distribution provided here is a significantly simplified model.

- Card 13 provides information on the phonon decomposition weights. For Fe-56, we use only the continuous distribution, and have no translational contribution and also do not make use of discrete oscillators.

  - The first value on Card 13 is the translational weight. Since we have no translational/diffusive componenent to Fe-56, this is set to 0
  - The second value is the diffusion coefficient for the translational component. This is also set to 0, since it will not be used.
  - The third value is the weight of the continuous distribution. The sum of the translational, continuous, and discrete oscillator weights must sum to 1. Since neither of these auxiliary components are used, the continuous weight is set to 1.

-------------------------------------------------------------------------------


**Card 14-16**

.. literalinclude:: exampleInputs/fe_singleTemp
   :language: html
   :lines: 1-34

Cards 14-16 define the discrete ocsillators that will be used to supplement the continuous frequency distribution. They are typically used to represent higher-energy peaks in the vibrational spectrum. 

The only value on Card 14 is the number of discrete oscillators to be used. Since we do not use any here, the Card 14 value is set to 0 and Cards 15-16 are omitted.

-------------------------------------------------------------------------------

**Cards 17-19**

- Cards 17-18 are only given for the liquid hydrogen or liquid deuterium cases, so we omit them here. 

- Card 19 provides the coherent scattering fraction, an effect that we indicated we would not use when we set Card 5's sixth value equal to 0. Thus we omit Card 19 as well.


-------------------------------------------------------------------------------


**Card 20**

.. literalinclude:: exampleInputs/fe_singleTemp
   :language: html
   :lines: 1-

- Card 20 is a set of comments that will be included in the final output tape (tape24). Card 20 will continue to be read until a blank line (consisting of only a "/") is read in.

  This final blank card indicates the end of LEAPR. However, we still have yet to tell NJOY that we wish to run no more modules. This is done by putting "stop" after the LEAPR input, which ends the NJOY run.
