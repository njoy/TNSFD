



**********************
Users Manual
**********************

.. contents:: 

Breakdown of Cards
================================================================



1 - Output File
----------------------------------------------------------------

a. :code:`nout` - Desired tape number for the LEAPR output file. Must have an absolute value between 20 and 99 inclusively. Can be positive (ASCII) or negative (binary). For example, "24" will correspond to the thermal scattering file being written to "tape24".
  
  .. note:: In NJOY, unit numbers from 20 through 99 are used for storing results or linking modules, units 10 through 19 are reserved for scratch files, which will be destroyed after a module has completed its job, and units below 10 are reserved for the system. Negative unit numbers indicate binary mode.


2 - Title
----------------------------------------------------------------
a. :code:`title` - Used to label the input deck and the output listing for the user's convenience. The title string does not go into the output ENDF file.



3 - General Run Control
----------------------------------------------------------------
a. :code:`ntempr` [**default = 1**] - Number of temperatures

..   Restrictions include:
       Positive integer 


b. :code:`iprint` [**default = 1**] - Print control.

   Possible values include:
       0 - Minimal verbosity

       1 - Standard verbosity

       2 - Most verbose 
    


c. :code:`nphon` [**default = 100**] - Phonon-expansion order. All LEAPR runs include a :ref:`continuous, solid-type calculation<continuous_solid_type>` which uses the phonon expansion method to generate a scattering law. This dictates the upper limit of the phonon expansion sum.

..   Restrictions include:
       Positive integer





4 - ENDF Output Information
----------------------------------------------------------------
a. :code:`mat` - ENDF material identification number. These numbers are available according to the ENDF standards. For convenience, they are summarized [LINK TO THERMAL SCATTERING PAGE].

   Restrictions include:
       Values corresponding to materials in the ENDF format.



  

b. :code:`za` - :math:`1000*z+a` for the principal scatterer, where :math:`z` is the atomic number and :math:`a` is the mass number.


c. :code:`isabt` [**default = 0**] - Flag indicating whether to output the non-symmetric or symmetric scattering law. 

   Possible values include:
       0 - Non-symmetric

       1 - Symmetric


d. :code:`ilog` [**default = 0**] - Flag indicating whether to output :math:`S(\alpha,\beta)` or :math:`\mathrm{log}_{10}[S(\alpha,\beta)]`. Giving the log of the scattering law is the ENDF-sanctioned way of handling very small numbers in File 7.


   Possible values include:
       0 - :math:`S(\alpha,\beta)`

       1 - :math:`\mathrm{log}[S(\alpha,\beta)]`

  


e. :code:`smin` [**default = 1e-75**] - Scattering law values lower than this will be set to 0.0. Only invoked if :code:`ilog=0`.





5 - Principal Scatterer Information
----------------------------------------------------------------
The "principal scatterer" may be hard to select for materials. For :math:`\mbox{H}_2\mbox{O}`, it's :math:`\mbox{H}`. For :math:`\mbox{ZrH}`, it would be :math:`H` for :code:`mat=7` and :math:`\mbox{Zr}` for :code:`mat=58`. For mixed moderators like :math:`\mbox{BeO}`, it is typically the lighter material. 

a. :code:`awr` - Atomic weight ratio between the neturon and the principal scatterer.

b. :code:`spr` - Free atom cross section for preincipal scatterer (in units of barns). This value should be chosen by looking at the low-energy limit for MF=3/MT=2 (elastic scattering) on the neutron file to be used with the new evaluation.

c. :code:`npr` - Number of principal scattering atoms in the compound. This would be 2 for :math:`\mbox{H}_2\mbox{O}`, and 1 for :math:`\mbox{BeO}`.

d. :code:`iel` [**default = 0**] - Coherent elastic options. This should typically be equal to 0, except for solid moderators. Currently, only five materials are supported (listed below). 

   Possible values include:
       0 - None (default)

       1 - Graphite
       
       2 - Beryllium
       
       3 - Beryllium Oxide
       
       4 - Aluminum (FCC)
       
       5 - Lead (FCC)
       
       6 - Iron (BCC)
       

 
e. :code:`ncold` [**default = 0**] - Cold hydrogen option. This should be set to 0 except when liquid hydrogen or liquid deuterium is considered. 

   Possible values include:
       0 - None (default)

       1 - Ortho Hydrogen
       
       2 - Para Hydrogen
       
       3 - Ortho Deuterium 
       
       4 - Para Deutrerium
       



d. :code:`nsk` [**default = 0 (none)**] - This should be set to 0 unless representation of intermolecular interference is desired. If :code:`nsk` is set to 1 or 2, Cards 17-19 will be required. 

   Possible values include:
       0 - None (default)

       1 - Vineyard 
       
       2 - Skold 
 


6 - Secondary Scatterer Information
----------------------------------------------------------------
Note that if you only have a principal scatterer and no secondary scatterers, Card 6 entry line should simply consist of :code:`0/`.

a. :code:`nss` - Number of secondary scatterers

   Possible values include:
       0 - No secondary scatterers

       1 - 1 secondary scatterer type
       
b. :code:`b7` - Flag indicating the treatment that will be applied to the secondary scatterer.

   Possible values include:
       0 - SCT approximation. This is most suitable for mixed moderators such as BeO and Benzine. In these cases, the entire scattering law for the molecule is provideded in MF=7/MT=4, and is intended to be used with the neutron file for the primary scatterer. The secondary scatterer's cross section, atomic weight ratio, and effective temperature are only used for extrending the scattering law with the SCT approximation. 

       1 - Free gas approximation. 

       2 - Diffusion Model
 
    When :code:`b7` is 1 or 2, only the scattering law for the primary scatterer is given, and the effects of the secondary scatterer are to be included later using an analytic law. 


c. :code:`aws` - Atomic weight ratio between the neturon and the secondary scatterer.


d. :code:`sps` - Free atom cross section for the secondary scatterer (units of barns).

e. :code:`mss` -  Number of secondary scatter atoms of this type in the compound. For :math:`\mbox{H}_2\mbox{O}`, the secondary scatterer would be :math:`\mbox{O}` and :code:`mss` would be equal to 1.



7 - :math:`\alpha,\beta` Input
----------------------------------------------------------------
a. :code:`nalpha` - Number of :math:`\alpha` values that will be provided in Card 9
b. :code:`nbeta` - Number of :math:`\beta` values that will be provided in Card 8
c. :code:`lat` [**default=0**] - Flag that indicates whether the :math:`\alpha` and :math:`\beta` values are scaled by :math:`0.0253/k_bT`, where :math:`k_bT` is the temperature in eV.


In the ENDF thermal format, the values for :math:`S(\alpha,\beta)` for higher temperatures are given on the same :math:`\alpha` and :math:`\beta` grids as is provided for the base temperature. However, :math:`\alpha` and :math:`\beta` are inversely proportional to temperature, so for high temperatures only the smaller :math:`\alpha` and :math:`\beta` values would be seen. This is a waster of space on the ENDF evaluation, so using a :code:`lat` value of 1 would spread the scattering law values for higher temperatures out, thereby giving a more accurate representation.




8 - :math:`\alpha` Values
----------------------------------------------------------------
:math:`\alpha` values are provided here in increasing order.

   Restrictions include:
       The number of :math:`\alpha` values provided must match the :code:`nalpha` input from Card 7.



9 - :math:`\beta` Values
----------------------------------------------------------------
:math:`\beta` values are provided here in increasing order.

   Restrictions include:
       The number of :math:`\beta` values provided must match the :code:`nbeta` input from Card 7.






10 - Temperature
----------------------------------------------------------------
For inputs with more than one temperature (:code:`ntempr` :math:`>0`), LEAPR uses a temperature loop, where Cards 10-18 are repeated for each temperature. Further explanaion of the temperature loop is provided below. 

For a given iteration in this temperature loop, Card 10 consists solely of the temperature in Kelvin.





11 - Phonon Distribution Control
----------------------------------------------------------------

The phonon distribution for the continuous, solid-type spectrum treatment is provided on an equally-spaced grid. 

a. :code:`delta` - Spacing of the phonon distribution (ev). Since the phonon distribution is provided on an equally spaced grid, this is a single value.

b. :code:`ni` - Number of phonon distribution values that will be provided on Card 12.



12 - Phonon Distribution
----------------------------------------------------------------
The phonon distribution is provided here. The phonon distribution does not need to be normalized, it will be normalized by LEAPR to the continuous, solid-type weight :math:`\omega_s`.

   Restrictions include:
       This distribution must be provided on an equally spaced grid, with the energy spacing equal to :code:`delta` from Card 11.
       The number of values provided here must match the :code:`ni` input from Card 11.





13 - Translational Control and Continuout Weight
----------------------------------------------------------------
As mentioned in :ref:`inelastic_scattering`, the phonon distribution is separated into a continuous contribution, and optional translational contribution, and an arbitrary number of discrete oscillators. 

a. :code:`twt` - Weight for the translational/diffusive contribution (:math:`\omega_t`)
b. :code:`c` - Diffusion constant for translational component. 

    Notes:
        If :code:`twt` is equal to zero, :code:`c` can be set to zero

        If :code:`twt` is greater than zero, then a setting :code:`c` to zero corresponds to a free gas translational calculation.
c. :code:`tbeta` - Weight for the continuous, solid-type spectrum (:math:`\omega_s`). 



Restrictions include:
       The translational weight :code:`twt`, the continuous, solid-type weight :code:`tbeta`, and the discrete oscillator weights (Card 14) must sum to 1.0.




14 - Discrete Oscillator Control
----------------------------------------------------------------
:code:`nd` - Number of discrete oscillators desired



15 - Discrete Oscillator Energies
----------------------------------------------------------------
Energy locations (in eV) for the discrete oscillators. 

Restrictions include:
    Must be :code:`nd` entries here. 



16 - Discrete Oscillator Weights
----------------------------------------------------------------
Weights of the discrete oscillators.

Restrictions include:
    Must be :code:`nd` entries here. 

    The translational weight :code:`twt`, the continuous, solid-type weight :code:`tbeta` (Card 13), and the discrete oscillator weights here must sum to 1.0.




17 - Static Structure Factor Control
----------------------------------------------------------------
This card is only given for liquid hydrogen or liquid deuterium cases. It controls the entry of the pair-correlation function used to account for intermolecular interference at very low neutron energies. 

a. :code:`nka` - Number of :math:`S(\kappa)` values that will be provided on Card 18.
b. :code:`dka` - :math:`\kappa` spacing for the :math:`S(\kappa)` entry on Card 18.

Restrictions include:
    Note that :code:`dka` is in units of inverse Angstrom



18 - Static Structure Factor
----------------------------------------------------------------
Static structure factor (pair correlation function) :math:`S(\kappa)` is provided here. 

Restrictions include:
    These values should correspond to an equally spaced, increasing :math:`\kappa` grid. 
    
    :math:`\kappa` is in units of inverse Angstrom.



19 - Coherent Scattering Fraction
----------------------------------------------------------------
:code:`cfrac` - Coherent scattering fraction. This is only invoked if :code:`nsk` from Card 5 is equal to 2.



20 - Comments 
----------------------------------------------------------------
The final section of the input deck gives the new comment cards to be added to the section MF=1/MT=451 on the ENDF file generated by LEAPR. If this section is to be a part of a standard library like ENDF/B-VII, there are standard fields that must appear. An example of the appearance of such a formal section will be found in the graphite example below. Note that the comment cards are terminated by an empty card; the number of cards entered is counted by LEAPR.







****************************
Structure of LEAPR
****************************

The general structure of the LEAPR source code is displayed below. This is not only helpful for understanding the code itself, but also in understanding the input formats. 


.. literalinclude:: exampleInputs/inputOverview
   :emphasize-lines: 6,18,22,25,29,32
   :language: none
   :linenos:
   :lineno-start: 0

.. .. literalinclude:: exampleInputs/inputOverview
   :language: html
   :emphasize-lines: 12,15-18
..    :lines: 1-3


There are a number of inputs that have the potential to change the structure of the LEAPR input file. We will walk through the ways in which the structure of the input file may vary according to calculations performed. 


The inputs that can alter the format of the input file are 

  ========================  ===============  =============
  Trait                     Dictated by...   Affects...
  ========================  ===============  =============
  Multiple Temperatures     :code:`ntempr`   Cards 10-19
  Discrete Oscillators      :code:`nd`       Cards 14-15
  Molecular Interference    :code:`nsk`      Cards 18-19
  Cold Hydrogen/Deuterium   :code:`ncold`    Card  18
  ========================  ===============  =============




Simplified Water Example
===========================

This example is a simplification of the "tsl-HinH2O.leapr" example from the ENDF-B/VIII.0 Thermal Scattering sublibrary. This example has been greatly simplified, and is intended only for instructional purposes. 

In this example, three temperatures are desired: 283.6 K, 350 K, and 600 K. The temperature loop (Cards 10-19) may be repeated in the input file. After the first iteration of the temperature loop, the any subsequent temperatures may be input as negative values to indicate that Cards 111-19 will be identical as the earlier values provided. In this example, we will not use this feature, but will rather provide Cards 11-19 separately for each temperature.

This water input uses discrete oscillators to represent two high energy peaks in the phonon distribution, so :code:`nd` from Card 14 is greater than 1. When this occurs, Cards 15-16 must be provided to detail the locations and weights of these oscillators.

If both molecular interference and cold-hydrogen/deuterium options are not used, then Cards 17-19 are not necessary, and can be omitted.

To summarize,

  ========================  ==========  =========================
  Trait                     Present?    Effect
  ========================  ==========  =========================
  Multiple Temperatures     Yes         Cards 10-19 get repeated
  Discrete Oscillators      Yes         Cards 15-16 are used
  Molecular Interference    No          No Cards 17-18
  Cold Hydrogen/Deuterium   No          No Cards 17-19
  ========================  ==========  =========================


.. literalinclude:: exampleInputs/endf8_water_simple
   :language: none
   :linenos:
   :lineno-start: 0


Let's walk through what is happening. First, as always, Cards 1-9 are read. These cards will never be repeated for a single LEAPR run. 

.. literalinclude:: exampleInputs/endf8_water_simple
   :language: none
   :linenos:
   :lines: 1-10
   :lineno-start: 0

Note that in these first nine cards, we specify that we will be wanting scattering data for three temperature (:code:`ntempr` (Card 3) is 3), that we need no molecular interference or cold hydrogen/deuterium consideration (:code:`nsk` and :code:`ncold` (Card 5) are zero).

Let's now go through our first temperature loop:

.. literalinclude:: exampleInputs/endf8_water_simple
   :language: none
   :lineno-start: 10
   :linenos:
   :lines: 11-21


We specify the temperature on Card 10 (since this is the first iteration, the temperature must be posibtively valued here). The phonon distribution for the continuous calculation is provided on Cards 11-12, and the translational/diffusive parameters are provided on Card 13. 

Card 14 shows :code:`nd` equal to two, meaning that we have to account for two discrete oscillators. The existence of oscillators mandates the use of Cards 15-16, since that's where the oscillator positions/weights are specified. 

Note that while technically the temperature loop extends from Card 10 to Card 19, Cards 17-19 are not used because they are useful for molecular interference / cold hydrogen, neither of which are necessary due to the aforementioned Card 5 inputs.


