



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



8 - :math:`\alpha` Values
----------------------------------------------------------------
:math:`\alpha` values are provided here in increasing order.




9 - :math:`\beta` Values
----------------------------------------------------------------
:math:`\beta` values are provided here in increasing order.




10 - Temperature
----------------------------------------------------------------
For inputs with more than one temperature (:code:`ntempr` :math:`>0`), LEAPR uses a temperature loop, where Cards 10-18 are repeated for each temperature. Further explanaion of the temperature loop is provided below. 

For a given iteration in this temperature loop, Card 10 consists solely of the temperature in Kelvin.





11 - Phonon Distribution Control
----------------------------------------------------------------
a. :code:``



12 - Phonon Distribution
----------------------------------------------------------------
a. :code:``




13 - Translational and Continuout Weights
----------------------------------------------------------------
a. :code:``




14 - Discrete Oscillator Control
----------------------------------------------------------------
a. :code:``



15 - Discrete Oscillator Energies
----------------------------------------------------------------
a. :code:``



16 - Discrete Oscillator Weights
----------------------------------------------------------------
a. :code:``



17 - Static Structure Factor Control
----------------------------------------------------------------
a. :code:``



18 - Static Structure Factor
----------------------------------------------------------------
a. :code:``



19 - Coherent Scattering Fraction
----------------------------------------------------------------
a. :code:``



20 - Comments 
----------------------------------------------------------------
a. :code:``



















.. literalinclude:: exampleInputs/inputOverview
   :language: html
..    :lines: 1-3

