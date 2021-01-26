


.. _usersManual:

**********************
Users Manual
**********************

.. .. contents:: 

.. Breakdown of Cards
.. ================================================================



Card 1 - Input & Output Files
----------------------------------------------------------------

In NJOY, unit numbers from 20 through 99 are used for storing results or linking modules, units 10 through 19 are reserved for scratch files, which will be destroyed after a module has completed its job, and units below 10 are reserved for the system. Negative unit numbers indicate binary mode. The following file specifications appear as numbers and correspond to those tapes (e.g. nendf = 20 corresponds to tape20). 


  .. list-table:: 
     :widths: 10 25 
     :header-rows: 0

     * - **nendf** 
       - ENDF tape for the MF7 format. 
     * - **nin**   
       - Old PENDF tape 
     * - **nout**
       -  New PENDF tape

  
Note that while :code:`nin` and :code:`nout` are required for each THERMR run, the :code:`nendf` specification is optional. If :code:`nendf` is set to zero, then no LEAPR input file will be read in, and a free gas scattering component will be used to create the output PENDF file :code:`nout`. If this option is exercised and :code:`nendf` is set to zero, then the inelastic option flag :code:`iin` of Card 2 may no be set to 2. 

..  .. note:: In NJOY, unit numbers from 20 through 99 are used for storing results or linking modules, units 10 through 19 are reserved for scratch files, which will be destroyed after a module has completed its job, and units below 10 are reserved for the system. Negative unit numbers indicate binary mode.


Card 2 - Material Information
----------------------------------------------------------------


  .. list-table:: 
     :widths: 10 25 
     :header-rows: 0

     * - **matde** 
       - Material ID on the ENDF tape
     * - **matdp**   
       - Material ID on the PENDF tape
     * - **nbin**
       - Number of equi-probable bins
     * - **ntemp**
       - Number of temperatures (default = 1)
     * - **iin**
       - | Inelastic options
         |      0 - None
         |      1 - Compute as free gas
         |      2 - Read :math:`S(\alpha,\beta)` and compute matrix
     * - **icoh**
       - | Elastic options
         |      0  - None
         |      1  - Graphite         (coherent)
         |      2  - Beryllium        (coherent)
         |      3  - Beryllium Oxide  (coherent)
         |      11 - Polyethylene     (incoherent)
         |      12 - H(ZrH)           (incoherent)
         |      13 - Zr(ZrH)          (incoherent)
     * - **iform**
       - | Ordering for Inelastic Scattering   
         |      0  - E-E'-mu
         |      1  - E-mu-E'
     * - **natom**
       - Number of principle atoms
     * - **mtref**
       - MT for the inelastic reaction (221-250 only)
     * - **iprint**
       - | Print option
         |      0  - Minimum
         |      1  - Maximum
         |      2  - Maximum, Normal + Intermediate results


Card 3 - Temperatures
----------------------------------------------------------------


  .. list-table:: 
     :widths: 10 25 
     :header-rows: 0

     * - **tempr** 
       - temperatures (Kelvin)




Card 4 - Limitations 
----------------------------------------------------------------


  .. list-table:: 
     :widths: 10 25 
     :header-rows: 0

     * - **tol** 
       - tolerance 
     * - **emax** 
       - maximum energy for thermal treatment. For temperatures greater than 3000.0, emax and the energy grid are scaled by temp/3000.0.) 

