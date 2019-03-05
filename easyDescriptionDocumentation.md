# EasyDescription
If you want to see what mkShapes will read from your *sample.py* configuration tou can 
expand it using *EasyDescription.py* script.

Example:

getSamplesFile(path , file ,True)-> Fill_path_to_File.root

Usage:

	easyDescription.py \
	--inputFileSamples=samples.py \
	--outputFileSamples=expandedScripts/expanded_samples.py
	
Or for *nuisances.py*:

	easyDescription.py \
	--inputFileNuisances=nuisances.py \
	--outputFileNuisances=expandedScripts/expanded_nuisances.py
	
You can use this script to see the samples used and the directory where they are stored.

Link to the script:
https://github.com/latinos/LatinoAnalysis/blob/33dc1f802a779493953422c874788e06e134c485/ShapeAnalysis/scripts/easyDescription.py

Example of output:
https://github.com/UniMiBAnalyses/PlotsConfigurations/blob/master/Configurations/VBS/2016Optimization/expandedScripts/expanded_samples.py