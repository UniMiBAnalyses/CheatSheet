# Latino Plot - Quick Guide 

## 0. Before starting

If the latino framework has not been installed yet follow this guide: https://docs.google.com/presentation/d/1-Hb5WXXzh-DvXmM1YBS-0j-YYFYemwJAPaaYzfXhlXw/edit?usp=sharing 


Before using the following commands make sure the *userConfig.py*
contain the correct path for *BaseDir*.

**N.B** : for enabling the following commands the **cmsenv** environment
variable is required:

	cd CMSSW_8_0_26_patch1/src/
	cmsenv
The following scripts have to be used in the directory where your *configuration.py*
is stored. 
	
## 1. EasyDescription
To see what mkShapes will read from your configuration you can 
expand *sample.py* (or *nuisances.py*) using the *easyDescription.py* script.

Usage:

	easyDescription.py \
	--inputFileSamples=samples.py \
	--outputFileSamples=expandedScripts/expanded_samples.py

If a directory (expandedScripts/) is used, you must create it before using these commands.
Or for *nuisances.py*:

	easyDescription.py \
	--inputFileNuisances=nuisances.py \
	--outputFileNuisances=expandedScripts/expanded_nuisances.py
	
You can use this script to check the samples used and the directory where they are stored.

**N.B** : *samples.py* is required as input if *nuisances.py* contains references to variables defined in *samples.py* 

Link to the script:
https://github.com/latinos/LatinoAnalysis/blob/33dc1f802a779493953422c874788e06e134c485/ShapeAnalysis/scripts/easyDescription.py

Example of output:
https://github.com/UniMiBAnalyses/PlotsConfigurations/blob/master/Configurations/VBS/2016Optimization/expandedScripts/expanded_samples.py

## 2. mkShapes
This step reads the post-processed latino trees (samples) and produces histograms 
for several variables and phase spaces (cuts).
It will create some preliminarily histogram (#histo=#cuts*#Variables)
and save the root file containing them in the **outpuDir**. This file
will be used by *mkPlot.py* and *mkDatacards*.

**Local Usage** (few samples only):

	mkShapes.py --pycfg=configuration.py

### 2.1 Submit jobs
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
	
### 2.2 Hadd the outputs	
If the command above is used, the output files will be split in different parts, 
depending on the number of jobs created. To merge these files use:

	mkShapes.py --pycfg=configuration.py \
	--batchSplit=AsMuchAsPossible \
	--doHadd=True
	
*NB*: If the --batchSplit=AsMuchAsPossible option is used, do not _hadd_
the outputs by hand but use the command above instead. Otherwise the MC 
statistical uncertainties will not be treated in the correct way.

Link to mkShapes.py code: https://github.com/latinos/LatinoAnalysis/blob/master/ShapeAnalysis/scripts/mkShapes.py

## 3. mkPlot & mkDatacrds

At this stage one can either produce plots or datacards.

### 3.1 Produce plots

Now we are ready to make data/MC comparison plots.

    mkPlot.py --inputFile=rootFile_test/plots_<tag>.root \
	--showIntegralLegend=1 \
	--scaleToPlot=1.9

The output directory where the plots will be saves is defined in configuration.py.
For more options look at the following link: https://github.com/latinos/LatinoAnalysis/blob/master/ShapeAnalysis/scripts/mkPlot.py

**N.B**: The plots will be generated using the root file created by mkShapes, so
the samples used in plot.py **MUST** be defined in samples.py.


### 3.2 Produce datacards

    mkDatacards.py --pycfg=configuration.py \
	--inputFile=rootFile_test/plots_<tag>.root

Link: https://github.com/latinos/LatinoAnalysis/blob/master/ShapeAnalysis/scripts/mkDatacards.py

**N.B**: The datacards will be generated using the root file created by mkShapes, so
the samples used in structure.py **MUST** be defined in samples.py.
