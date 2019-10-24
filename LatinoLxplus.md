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

It defines where the jobs will be stored

    #!/usr/bin/env python
    baseDir  = '/afs/cern.ch/user/x/xjanssen/cms/HWW2015/'       #    <--- the base directory
    jobDir   = baseDir+'jobs/'
    workDir  = baseDir+'workspace/'

(is this used only for post-processing?)


## 1. Get Configurations repository

Get the configurations repository, where the cuts, samples, nuisances, ... are defined:

    git clone git@github.com:UniMiBAnalyses/PlotsConfigurations.git
    
If the central configuration is needed instead of the "Unimib" one, do this instead:

    git clone git@github.com:latinos/PlotsConfigurations.git

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

TBU !!!

This step reads the post-processed latino trees (samples) and produces histograms 
for several variables and phase spaces (cuts).
It will create some preliminarily histogram (#histo=#cuts*#Variables)
and save the root file containing them in the **outpuDir**. This file
will be used by *mkPlot.py* and *mkDatacards*.

**Local Usage** (few samples only):

        mkShapes.py --pycfg=configuration.py

### 3.1 Submit jobs
If you have a lot of samples you can submit the jobs on batch:

        mkShapes.py --pycfg=configuration.py \
        --batchSplit=AsMuchAsPossible \
        --doBatch=True
If you are not using the "True" statement in getSamplesFile(Dir, file , **True**), you need to add to the command above:

        --inputDir=path_To_Samples        
 
The jobs can take a while, thus to check their status:

    mkBatch.py --status
or alternatively: 

        qstat

After all your jobs are finished, and before going to the next step, check the .jid files 
in the following output directory (**tag** is specified in *configuration.py* , **BaseDir** is defined
in the *userConfig.py* file):

    ls -l <BaseDir>/jobs/mkShapes__tag/*.jid
    
If you find .jid files it means that the corresponding jobs failed, check the .err and .out 
files to understand the reason of the failure.

If a job takes too long / fails, one can kill it and resubmit manually, e.g.:

    qsub <BaseDir>/jobs/mkShapes__tag/file.sh

If several jobs failed and you want to resubmit them all at once you can do:

    cd <BaseDir>/jobs/mkShapes__tag
    for i in *jid; do qsub ${i/jid/sh}; done
        
### 3.2 Hadd the outputs        
If the command above is used, the output files will be split in different parts, 
depending on the number of jobs created. To merge these files use:

        mkShapes.py --pycfg=configuration.py \
        --batchSplit=AsMuchAsPossible \
        --doHadd=True
        
*NB*: If the --batchSplit=AsMuchAsPossible option is used, do not _hadd_
the outputs by hand but use the command above instead. Otherwise the MC 
statistical uncertainties will not be treated in the correct way.

Link to mkShapes.py code: https://github.com/latinos/LatinoAnalysis/blob/master/ShapeAnalysis/scripts/mkShapes.py

## 4. mkPlot & mkDatacrds

At this stage one can either produce plots or datacards.

### 4.1 Produce plots

Now we are ready to make data/MC comparison plots.

    mkPlot.py --inputFile=rootFile_test/plots_<tag>.root \
        --showIntegralLegend=1 \
        --scaleToPlot=1.9

The output directory where the plots will be saves is defined in configuration.py.
For more options look at the following link: https://github.com/latinos/LatinoAnalysis/blob/master/ShapeAnalysis/scripts/mkPlot.py

**N.B**: The plots will be generated using the root file created by mkShapes, so
the samples used in plot.py **MUST** be defined in samples.py.


### 4.2 Produce datacards

    mkDatacards.py --pycfg=configuration.py \
        --inputFile=rootFile_test/plots_<tag>.root

Link: https://github.com/latinos/LatinoAnalysis/blob/master/ShapeAnalysis/scripts/mkDatacards.py

**N.B**: The datacards will be generated using the root file created by mkShapes, so
the samples used in structure.py **MUST** be defined in samples.py.
