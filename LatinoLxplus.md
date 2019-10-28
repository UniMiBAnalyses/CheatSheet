# Latino Plot - Quick Guide 

Instructions based on Full run II analyses, performed on lxplus

PlotConfiguration from https://github.com/UniMiBAnalyses/

Code from original https://github.com/latinos


## 0. Before starting

Suggestion: make a clean folder in lxplus. Organize things in folders/subfolders.

If the latino framework has not been installed:


    cmsrel CMSSW_10_2_15_patch2
    cd CMSSW_10_2_15_patch2/src/
    cmsenv
    
    git clone --branch 13TeV-AM-Instructions  git@github.com:latinos/setup.git LatinosSetup
    
    source LatinosSetup/SetupShapeOnly.sh
    
    scramv1 b -j 20

    
NB: the environment is setup with **cmsenv**.
After the first installation you can skip the git clone, and scramv1 (equivalent of "make", it compiles the code),
but you will always have to setup the environment with

    cmsenv
    
It will setup the environment of the folder where you currently are.

Before using the following commands make sure the *userConfig.py*
contain the correct path for *BaseDir*.
A template is available in:

    LatinoAnalysis/Tools/python/userConfig_TEMPLATE.py
    
just rename it to:

    LatinoAnalysis/Tools/python/userConfig.py

It defines where the jobs will be stored (for condor submission):

    #!/usr/bin/env python
    baseDir  = '/afs/cern.ch/user/x/xjanssen/cms/HWW2015/'       #    <--- the base directory
    jobDir   = baseDir+'jobs/'
    workDir  = baseDir+'workspace/'



## 1. Get Configurations repository

Get the configurations repository, where the cuts, samples, nuisances, ... are defined:

    git clone git@github.com:UniMiBAnalyses/PlotsConfigurations.git
    
If the central configuration is needed instead of the "Unimib" one, do this instead:

    git clone git@github.com:latinos/PlotsConfigurations.git

You could also fork the repository in your own github and get that version.
    
If you do "ls" in src/ now you should have something like

    LatinoAnalysis  LatinosSetup  MelaAnalytics  PhysicsTools  PlotsConfigurations  ZZMatrixElement


 
The following scripts have to be used in the directory where your *configuration.py*
is stored. 


## 2. EasyDescription
To see what mkShapes will read from your configuration you can 
expand *sample.py* (or *nuisances.py*) using the *easyDescription.py* script.

Usage:

        easyDescription.py \
        --inputFileSamples=samples.py \
        --outputFileSamples=expanded_samples.py

Or for *nuisances.py*:

        easyDescription.py \
        --inputFileNuisances=nuisances.py \
        --outputFileNuisances=expanded_nuisances.py
        
You can use this script to check the samples used and the directory where they are stored.

**N.B** : *samples.py* is required as input if *nuisances.py* contains references to variables defined in *samples.py* 

Link to the script:

    https://github.com/latinos/LatinoAnalysis/blob/master/ShapeAnalysis/scripts/easyDescription.py

Example of output:

    https://github.com/UniMiBAnalyses/PlotsConfigurations/blob/master/Configurations/VBS/2016Optimization/expandedScripts/expanded_samples.py

    
## 3. mkShapes/mkShapeMulti

This step reads the post-processed latino trees (samples) and produces histograms 
for several variables and phase spaces (cuts).
It will create some preliminarily histogram (#histo=#cuts*#Variables)
and save the root file containing them in the **outpuDir**. This file
will be used by *mkPlot.py* and *mkDatacards.py*.

**Local Usage** (few samples only):

    mkShapesMulti.py --pycfg=configuration.py --batchSplit=Samples,Files

This is extramely slow, but good for testing.

**Submission** (few samples only):

Produce shapes:

    mkShapesMulti.py --pycfg=configuration.py --doBatch=1 --batchSplit=Samples,Files --batchQueue=espresso
    mkShapesMulti.py --pycfg=configuration.py --doBatch=1 --batchSplit=Samples,Files --batchQueue=workday 

    
Check if jobs are done by doing:

    condor_q
    
Add root files:

    mkShapesMulti.py --pycfg=configuration.py --doHadd=1 --batchSplit=Samples,Files
    mkShapesMulti.py --pycfg=configuration.py --doHadd=1 --batchSplit=Samples,Files  --nThreads=6
    
If this is too slow try to hadd manually (TAG is the one in configuration.py)

    cd rootFileTAG
    hadd -j 5 -f plots_ggH_TAG_ALL.root plots_ggH_TAG_ALL_* 

    
## 4. plots

Make plots:

    mkPlot.py --pycfg=configuration.py --inputFile=rootFileTAG/plots_TAG_ALL.root

For unblinding the control regions, comment out the signal regions in cuts.py and set isBlind=0 in plot.py. Then rerun mkPlot.py as above. 

**N.B**: The plots will be generated using the root file created by mkShapes, so
the samples used in plot.py **MUST** be defined in samples.py.


## 5. Datacards

Make datacards:

    mkDatacards.py --pycfg=configuration.py --inputFile=rootFileTAG/plots_TAG_ALL.root

Make combination of datacards and workspaces by editing the script 'scripts/doCombination.sh' and running:

    ./doCombination.sh

**N.B**: The datacards will be generated using the root file created by mkShapes, so
the samples used in structure.py **MUST** be defined in samples.py.
