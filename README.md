MadGraph Gridpack Producer For CMSSW
====================================

This program contains input cards for MadGraph (more specifically, MadGraph5_aMC@NLO) 
and programs that use these cards to produce gridpacks for Monte Carlo production in CMSSW. 
For a more complete and update date gridpack generator that can use programs other than MadGraph, 
please refer to https://github.com/cms-sw/genproductions/tree/pre2017 and for more in detail 
instructions and documentation, please refer to https://twiki.cern.ch/twiki/bin/viewauth/CMS/QuickGuideMadGraph5aMCatNLO 

Instructions
============

These programs should be run on CERN's lxplus or Fermilab's lpc. Gridpacks must be created
outside of CMSSW and without the cmsenv. For an example on how to use these gridpacks to 
produce root files, please see https://github.com/bregnery/hhMCgenerator

Installation
------------

To obtain these programs, simply clone this git repository

    git clone https://github.com/bregnery/MadGraphCardsForCMSSW

Gridpack Generation
-------------------

To generate a gridpack, first update permissions to run shell scripts

    chmod u+x gridpack_generation.sh

Then, update gridpack_generation.sh to make sure all fifo pipes are directed to /tmp directory.
Next, generate a gridpack using the desired data cards

    ./gridpack_generation.sh <name of process card without _proc_card.dat> <folder containing cards relative to current location>

For example, 

    ./gridpack_generation.sh Radion_hh_WWWW_jets_narrow_M3500 cards/Radion_hh_WWWW_jets_narrow_M3500/

### Using Cluster to Create Gridpacks

To submit jobs on lxplus and store them locally, use the submit_gridpack_generation_local.sh

    ./submit_gridpack_generation_local.sh <memory> <queue for master job> <name of process card without _proc_card.dat> <folder containing cards relative to current location> <queue>

For example,

    ./submit_gridpack_generation_local.sh 15000 2nw Radion_hh_WWWW_jets_narrow_M3500 cards/Radion_hh_WWWW_jets_narrow_M3500/ 8nh
 
Creating/Editing Data Cards
---------------------------

When creating or editing data cards, make sure to create four cards with the name as your repository.

    <repository>_proc_card.dat
    <repository>_run_card.dat
    <repository>_customizecards.dat
    <repository>_extramodels.dat

Make sure to less models needed in extra models if running beyond Standard Model. Number of events is 
listed listed in run_card.dat. When using the gridpacks DO NOT generate more events than what is listed 
in run_card.dat.
