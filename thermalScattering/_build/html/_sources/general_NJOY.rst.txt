
**********************
NJOY Introduction 
**********************

..
  COMMENT: .. contents:: Table of Contents

NJOY Overview
=====================
The NJOY Nuclear Data Processing System is a comprehensive computer code package for producing pointwise and multigroup cross sections and related quantities from evaluated nuclear data in the ENDF format. NJOY works with evaluated files for incident neutrons, photons, and charged particles, producing libraries for a wide variety of particle transport and reactor analysis codes

The NJOY code consists of a set of 24 main modules, each performing a well-defined processing task. These modules are essentially separate computer programs, that can interact with each other by input and output files. The modules are supported by a number of subsidiary modules providing things like physics constants, utility routines, and mathematics subroutines that can be “used” by the main modules. 


NJOY Example 
=====================


NJOY input files are able to call multiple modules in sequence, which can be used together to perform complicated manipulations of the nuclear data. Broadly speaking, an NJOY input file will be structured as follows.

.. literalinclude:: exampleInputs/genericInput
  :language: html

Here, the first module name is specified, and the inputs are divided into "cards" (i.e., lines of input). Each module has its own number of possible cards, and each card has its own number of inputs. Modules are called in the order that they appear on this input file, so Module 2 can accept the output of Module 1. 

Lines of NJOY input files may not exceed 80 characters, so if an line of input needs multiple lines, they may do so (this is shown in Module 2 Card 3 above). Any characters folloring a single forawrd slash is considered a comment and will not be read as input.

Many modules in NJOY cannot be called in isolation, as they require the output of some other module as input. LEAPR, however, can be called alone, as it does not require any auxiliary input files (just the input file is sufficient to call LEAPR).









