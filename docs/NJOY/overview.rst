
**********************
NJOY Introduction 
**********************

..
  COMMENT: .. contents:: Table of Contents

Overview
=====================
The NJOY Nuclear Data Processing System is a comprehensive computer code package for producing pointwise and multigroup cross sections and related quantities from evaluated nuclear data in the ENDF format. NJOY works with evaluated files for incident neutrons, photons, and charged particles, producing libraries for a wide variety of particle transport and reactor analysis codes

The NJOY code consists of a set of 24 main modules, each performing a well-defined processing task. These modules are essentially separate computer programs, that can interact with each other by input and output files. The modules are supported by a number of subsidiary modules providing things like physics constants, utility routines, and mathematics subroutines that can be “used” by the main modules. 


Tapes
=====================

In NJOY, unit numbers from 20 through 99 are used for storing results or linking modules, units 10 through 19 are reserved for scratch files, which will be destroyed after a module has completed its job, and units below 10 are reserved for the system. Negative unit numbers indicate binary mode.



