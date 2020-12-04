.. This is a comment. Note how any initial comments are moved by
   transforms to after the document title, subtitle, and docinfo.

.. demo.rst from: http://docutils.sourceforge.net/docs/user/rst/demo.txt

.. .. |EXAMPLE| image:: _images/temp.png
..    :width: 1em

------------------------------------------
H in H2O (Single temperature)
------------------------------------------



This example serves as a *very* simplified input that would allow a user to prepare the thermal scattering law :math:`S(\alpha,\beta)` for describing hydrogen bound in water. These values are for instructional purposes only. Note that parentheses following the forward slash will indicate the card number.

..
  COMMENT: .. contents:: Table of Contents
   :emphasize-lines: 1


-------------------------------------------------------------------------------


**Cards 1-2**

.. literalinclude:: exampleInputs/simple_H_H2O
   :language: html
   :lines: 1-3

- The zeroth line defines the module, which is LEAPR. 
- Typically, the first card is used to specify input and output files, however since LEAPR does not read in any auxiliary files, only the output file need be specified. In this example, the output file will be located in the (unless otherwise specified) bin directory as "tape24".
- The second line (card 2) contains the descriptive title that will be used in the final LEAPR output. 

.. -------------------------------------------------------------------------------

.. .. literalinclude:: exampleInputs/simple_H_H2O
..    :language: html
..    :lineno-start: 0
..    :lines: 1-3


-------------------------------------------------------------------------------

**Card 3**

.. literalinclude:: exampleInputs/simple_H_H2O
   :language: html
   :lines: 1-4

- Here, we want to process the material at a single temperature, so the number of temperatures is set to 1. 
- In addition to the output file (for us, tape24), NJOY also returns a summary output file, which is traditionally labeled "output". To control the amount of detail used when preparing this document, the second input of card 3 is the print control option. This value can be (0,1,2) which indicate increasing level of detail. 
- Every LEAPR run requires that the incoherent scattering component be calculated via phonon expansion method (discrete oscillators and/or diffusive behavior can be included, if requested). Thus, the final input value is the phonon expansion number, which indicates the number of terms :math:`N` that should be computed when approximating the sum in :ref:`the phonon expansion method<continuous_solid_type>`.

.. math:: 
    S^{(s)}_{n.sym}(\alpha,\beta) \approx \mathrm{e}^{-\alpha\lambda_s}\sum_{n=0}^N \frac{\alpha^n}{n!} W_n(\beta)






-------------------------------------------------------------------------------

**Card 4**

.. literalinclude:: exampleInputs/simple_H_H2O
   :language: html
   :lines: 1-5

- Every material has an ENDF-specified identification number to describe the scattering material. Note that these MAT numbers that describe *materials* are separate from those that describe *individual atoms*. 
  
    For example, the MAT number for :math:`^1\mbox{H}` is 125, according to https://t2.lanl.gov/nis/data/endf/endfvii-n.html, whereas the MAT number for water is 1, according to https://oecd-nea.org/dbdata/data/manual-endf/endf102.pdf. For convenience, the currently recognized MAT numbers for commonly occuring materials are provided below.
  
  +---------------+-----+---------------+-----+---------------+-----+
  | Compount      | MAT | Compound      | MAT | Compound      | MAT |
  +===============+=====+===============+=====+===============+=====+
  | :math:`\mbox  | 1   | :math:`\mbox  | 27  | :math:`\mbox  | 46  |
  | {H}_2\mbox    |     | {BeO}`        |     | {O}` in       |     |
  | {O}`          |     |               |     | :math:`\mbox  |     |
  |               |     |               |     | {BeO}`        |     |
  +---------------+-----+---------------+-----+---------------+-----+
  | Cold          |     | :math:`\mbox  | 28  | :math:`\mbox  | 47  |
  | :math:`^1_1   |     | {Be}_2\mbox   |     | {O}` in       |     |
  | \mbox{H}`     |     | {C}`          |     | :math:`\mbox  |     |
  | (Para)        | 2   |               |     | {SiO}_2`      |     |
  +---------------+-----+---------------+-----+---------------+-----+
  | Cold          |     | :math:`\mbox  | 29  | :math:`\mbox  | 48  |
  | :math:`^1_1   |     | {Be}` in      |     | {O}` in       |     |
  | \mbox{H}`     |     | :math:`\mbox  |     | :math:`\mbox  |     |
  | (Ortho)       | 3   | {BeO}`        |     | {UO}_2`       |     |
  +---------------+-----+---------------+-----+---------------+-----+
  | :math:`\mbox  | 7   | Graphite      | 31  | :math:`\mbox  | 53  |
  | {H}` in       |     |               |     | {Al}` metal   |     |
  | :math:`\mbox  |     |               |     |               |     |
  | {ZrH}`        |     |               |     |               |     |
  +---------------+-----+---------------+-----+---------------+-----+
  | :math:`\mbox  | 11  | Liquid        | 33  | :math:`\mbox  | 56  |
  | {D}_2\mbox    |     | Methane       |     | {Fe}` metal   |     |
  | {O}`          |     |               |     |               |     |
  +---------------+-----+---------------+-----+---------------+-----+
  | Cold          | 12  | Solid         | 34  | :math:`\mbox  | 58  |
  | :math:`^1_2   |     | Methane       |     | {Zr}` in      |     |
  | \mbox{D}`     |     |               |     | :math:`\mbox  |     |
  | (Para)        |     |               |     | {ZrH}`        |     |
  +---------------+-----+---------------+-----+---------------+-----+
  | Cold          | 13  | Polyethylene  | 37  | :math:`\mbox  | 75  |
  | :math:`^1_2   |     |               |     | {UO}_2`       |     |
  | \mbox{D}`     |     |               |     |               |     |
  | (Ortho)       |     |               |     |               |     |
  +---------------+-----+---------------+-----+---------------+-----+
  | :math:`\mbox  | 26  | Benzine       | 40  | :math:`\mbox  | 76  |
  | {Be}` metal   |     |               |     | {UC}`         |     |
  +---------------+-----+---------------+-----+---------------+-----+

..  +---------------+-----+----------------------+-----+
  | Compount      | MAT | Compount             | MAT |
  +===============+=====+======================+=====+
  | Water         | 1   | | Liquid Methane     | 33  |
  +---------------+-----+----------------------+-----+
  | Para          | 2   | | Solid Methane      | 34  |
  | Hydrogen      |     |                      |     |
  +---------------+-----+----------------------+-----+
  | Ortho         | 3   | | Polyethylene       | 37  |
  | Hydrogen      |     |                      |     | 
  +---------------+-----+----------------------+-----+
  | :math:`\mbox  |     | | Benzine            | 40  |
  | {H}` in       |     |                      |     |
  | :math:`\mbox  |     |                      |     |
  | {ZrH}`        |     |                      |     |
  +---------------+-----+----------------------+-----+
  | Heavy Water   |     | :math:`\mbox{O}` in  | 46  |
  |               |     | :math:`\mbox{BeO}`   |     | 
  +---------------+-----+----------------------+-----+
  | Para          |     | :math:`\mbox{O}` in  | 47  |
  | Deuterium     |     | :math:`\mbox{SiO}_2` |     |
  +---------------+-----+----------------------+-----+
  | Ortho         |     | :math:`\mbox{O}` in  | 48  |
  | Deuterium     |     | :math:`\mbox{UO}_2`  |     | 
  +---------------+-----+----------------------+-----+
  | Beryllium     |     | Aluminum metal       | 53  |
  | Metal         |     |                      |     | 
  +---------------+-----+----------------------+-----+
  | Beryllium     |     | Iron metal           |     |
  | Oxide         |     |                      |     |
  +---------------+-----+----------------------+-----+
  | Beryllium     |     | :math:`\mbox{Zr}` in | 58  |
  | Carbide       |     | :math:`\mbox{ZrH}`   |     |
  +---------------+-----+----------------------+-----+
  | :math:`\mbox  |     | :math:`\mbox{UO}_2`  | 75  |
  | {Be}` in      |     |                      |     |
  | :math:`\mbox  |     |                      |     |
  | {BeO}`        |     |                      |     |
  +---------------+-----+----------------------+-----+
  | Graphite      |     | :math:`\mbox{UC}`    | 76  |
  +---------------+-----+----------------------+-----+


- The second input is the :math:`ZA` value, which is another value used to identify materials. For the case of :math:`\mbox{H}` in :math:`\mbox{H}_2\mbox{O}`, this is equal to 101 as can be seen by the following rules:

    For isotopes, :math:`ZA` is equal to :math:`1000\,Z+A` where :math:`Z` and :math:`A` are the charge number and mass number. If the material is an element that has more than one naturally occurring isotope, then :math:`ZA` is equal to :math:`1000\,Z`. If the material is a compound, then :math:`ZA` is equal to :math:`ZA=\mbox{MAT}+100`.


.. - The second input is the :math:`ZA` value, which is another value used to identify materials. 
  - For isotopes, :math:`ZA` is equal to :math:`1000\,Z+A` where :math:`Z` and :math:`A` are the charge number and mass number. 
  .. , respectively (e.g. :math:`ZA` for :math:`^{238}_{92}\mbox{U}` is 92238.0, and ZA for :math:`^{9}_{4}\mbox{Be}` is 4009.0. 
  - If the material is an element that has more than one naturally occurring isotope, then :math:`ZA` is equal to :math:`1000\,Z`.
  .. For example, :math:`ZA` for the element Tungsten :math:`_{74}W` is 74000.0.  
  - If the material is a compound, then :math:`ZA` is equal to :math:`ZA=\mbox{MAT}+100`.
  Thus, for the case of :math:`\mbox{H}` in :math:`\mbox{H}_2\mbox{O}`, :math:`ZA=\mbox{MAT}+100=101`.

- The third input on card 4 is a flag for what "type" of scattering law (symmetric vs. non-symmetric) to output. A value of 0 corresponds to symmetric, whereas a value of 1 corresponds to non-symmetric. Note that if the non-symmetric scattering law is chosen, then in actuality :math:`S_{n.sym}(\alpha,-\beta)` will be returned (this is because the positive side of the non-symmetric scattering law becomes prohibitively small and thus hard to store).

  Recall that the symmetric and non-symmetric scattering laws are related to each other by 

  .. math:: 
    S_{sym}(\alpha,\beta)=\mathrm{e}^{\beta/2}~S_{n.sym}(\alpha,\beta)

  and that 

  .. math:: 
    S_{n.sym}(\alpha,\beta)=\mathrm{e}^{-\beta}~S_{n.sym}(\alpha,-\beta)

 Lastly, it is worth nothing that if a value of 1 is chosen here (indicating a non-symmetric scattering law), that the output file **cannot** be processed by the THERMR module. [MAKE SURE THAT THIS IS CORRECT]

- The fourth entry on card 4 is a flag for whether the output file should contain :math:`S(\alpha,\beta)` or :math:`\mbox{log}_{10}\big[S(\alpha,\beta)\big]` (which correspond to an entry value of 0 or 1, respectively). Writing results in log form is a standard ENDF approach of handling very small numbers for thermal scattering.  

- The last entry on card 4 is the minimum value of :math:`S(\alpha,\beta)` to store. 



-------------------------------------------------------------------------------

**Card 5**

.. literalinclude:: exampleInputs/simple_H_H2O
   :language: html
   :lines: 1-6

LEAPR allows for either 1 or 2 scattering species to be considered in the same run. Card 5 is focused on the materials primary scatterer. If there is a secondary scatterer considered, that will be specified on the following card.  

- The first value is the atomic weight ratio of the primary scatterer (AWR), which is defined as the ratio of the mass of the material to that of the neutron. For hydrogen in water, this is about 0.99917.

- The second value is the free atom scattering cross section :math:`\sigma_b` for the primary scatterer (which in this example is hydrogen). These values can be obtained at https://www.nndc.bnl.gov/sigma under "resonance parameters - interpreted". 

- The number of primary scattering atoms in the material. For water, there are two hydrogens.

- The fourth value is a flag for coherent elastic scattering (Bragg edges). It can be 0 or 1. A value of 0 is chosen which indiates no coherent elastic calculation.

- The fifth value is a cold hydrogen/deuterium flag, which dictates whether or not nuclear spins can be assumed to be distributed randomly. In most cases, this flag will be 0, indicating that spins are randomly distributed (i.e. the material is not cold hydrogen or cold deuterium).

- The final value defines whether intermolecular coherence will be accounted for, and if so, how it will be approximated. If 0 is chosen, no intermolecular coherence will be considered, whereas 1 and 2 indicate that the Vineyard and Skold approximations will be used, respectively. If the latter two options are used, Cards 17-18 must be provided, and Card 19 must also be provided if a value of 2 is chosen (Skold).


-------------------------------------------------------------------------------

**Card 6**

.. literalinclude:: exampleInputs/simple_H_H2O
   :language: html
   :lines: 1-7

This card is focused on the secondary scatterer, if applicable. 

- This is the number of secondary scatterers in a material. For water, there is a single oxygen atom in a molecule, this this is set to 1. Note that values above 1 are not allowed.

- The second input dictates how to describe the scattering of this secondary species. This entry can take a value of 0, 1, or 2 corresponding to short-collision time (SCT), free, or diffusion respectively. Oxygen in water is described as a free gas, thus a value of 1 is chosen. 

- The third entry is the atomic weight ratio (AWR) of the secondary scatterer.

- The fourth entry is the free scattering cross section :math:`\sigma_b` for the secondary scatterer. 

- [WAIT YEAH NO DEFINITELY TRY TO UNDERSTAND THIS CARD BETTER, YOU'RE JUST TOO TIRED RIGHT NOW]


-------------------------------------------------------------------------------

**Card 7-9**

.. literalinclude:: exampleInputs/simple_H_H2O
   :language: html
   :lines: 1-20

LEAPR prepares the scattering law :math:`S(\alpha,\beta)` for a user-defiend grid of :math:`\alpha` and :math:`\beta` values. 

- Card 7 defines the number of :math:`\alpha` values (22), the number of :math:`\beta` values (28) and whether the :math:`\alpha,\beta` grids should be scaled. If the scaling option is set to 0, neither grid is scaled. Since it is set to 1, however, both grids will be scaled by :math:`0.0253/k_bT` where :math:`k_bT` is the temperature in eV. 

- Card 8 provides the :math:`\alpha` values, and Card 9 provides the :math:`\beta` values. For lines with many values of inputs, such as Cards 8 and 9 here, the input values can span multiple lines since LEAPR was already informed of the number of :math:`\alpha` and :math:`\beta` values to expect in Card 7.


Note that, as seen above, a blank line can be added between lines of LEAPR input to separate cards. 

-------------------------------------------------------------------------------

**Card 10-12**

.. literalinclude:: exampleInputs/simple_H_H2O
   :language: html
   :lines: 1-37

- Card 10 provides the desired temperature in K.

- Cards 11 and 12 define the vibrational frequency spectrum (phonon distribution, phonon density of states, etc) that will be used in the continuous, phonon expansion calculation. The frequency distribution is provided on a uniformly spaced energy grid (energy grid has units of eV). 

  - The first entry of Card 11 is the energy spacing on this grid, and the second entry is the number of values in this frequency distribution. 

  - Card 12 provides the frequency distribution values. Note that the first and last values should be 0.0. The distribution provided here is a significantly simplified model.


-------------------------------------------------------------------------------

**Card 13**

.. literalinclude:: exampleInputs/simple_H_H2O
   :language: html
   :lines: 1-38

When processing incoherent scattering, LEAPR processes the vibrational frequency spectrum from Card 12 in the phonon expansion. If requested, two additional effects can be considered: the effect of discrete ocsillators and the effect of some diffusive behavior. Card 13 defines how much, if any, attention should be paid to the diffusive nature of the material.

To combine the effects of continuous, diffusive, and discrete-oscillator behavior, each of these three components is assigned a weight, and these weights must add to 1.

- The first entry of card 13 is the translation weight.

- The second entry is the diffusion coefficient, which is set to zero for this model.

- The third entry is the continuous distribution weight. 

According to these input, the translative/diffusive behavior will be weighted by 0.05 andthe continuous, solid-type behavior will be weighted by 0.45. Since these add up to 0.5, that means that the weighting of the discrete oscillators (which will be defined shortly) must add to an additional 0.5.

-------------------------------------------------------------------------------

**Card 14-16**

.. literalinclude:: exampleInputs/simple_H_H2O
   :language: html
   :lines: 1-41

Cards 14-16 define the discrete ocsillators that will be used to supplement the continuous frequency distribution. They are typically used to represent higher-energy peaks in the vibrational spectrum. 

- Card 14 only has a single entry, indicating the number of discrete oscillators that will be used.

- Card 15 contains the energy locations (eV) of these two discrete ocsillators. 

- Card 16 contains the weights that each of these discrete ocsillators has. Since our translational weight and continuous weight add to 0.5, that means that the sum of these oscillator weights must add to 0.5 so that the total weighting sum will combine to 1.0.

-------------------------------------------------------------------------------

**Card 20**

.. literalinclude:: exampleInputs/simple_H_H2O
   :language: html
   :lines: 1-

*Cards 17-19 are invoked when an inelastic coherent approximation is requested. Since no intermolecular coherence was requested (i.e. the final value on card 5 is set to 0), these cards are omitted. Instead, we continue directly to card 20.*

- Card 20 is a set of comments that will be included in the final output tape (tape24). Card 20 will continue to be read until a blank line (consisting of only a "/") is read in.

  This final blank card indicates the end of LEAPR. However, we still have yet to tell NJOY that we wish to run no more modules. This is done by putting "stop" after the LEAPR input, which ends the NJOY run.
