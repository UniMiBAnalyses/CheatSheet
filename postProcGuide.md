# Postprocessing guide for [LatinoAnalysis NanoGardener](https://github.com/latinos/LatinoAnalysis/tree/master/NanoGardener)


### Step Zero

Try to run `eos ls /eos/user/INITIAL-OF-YOUR-NAME/YOUR-ACCOUNT/`. If it raises an exeption you should add a simple line in your `.bashrc` or `.zshrc`: 
`export EOS_MGM_URL=root://eoshome-INITIAL-OF-YOUR-NAME.cern.ch` and then source your bashrc/zshrc.
This sets the right redirector of your EOS. If also with this fix you get an error try with the following: `root://eosuser.cern.ch`.
Now that you know what your redirector is, you can use eos and xrdcp without any trouble. 

---


In order to produce 102X nanoAOD, one should use 10_2_X or newer release

<!-- export SCRAM_ARCH=slc6_amd64_gcc630 -->

```
cmsrel CMSSW_10_6_4
cd CMSSW_10_6_4/src
cmsenv
git clone --branch 13TeV git@github.com:latinos/setup.git LatinosSetup
source LatinosSetup/SetupShapeOnly.sh
scram b
```
<!-- Si può usare anche CMSSW_10_6_4 -->

Copy the file LatinoAnalysis/Tools/python/userConfig_TEMPLATE.py to LatinoAnalysis/Tools/python/userConfig.py and edit it to reflect your local paths.

---
Now we will be editing some files in `LatinoAnalysis/NanoGardener/python/framework`
### First step
Change the Sites_cfg.py. The content with key 'cern' is the one you will be using and should point to your EOS output folder (i.e. where your post processed ntuples will be saved). 
 Specify the EOS url you used in step zero as `xrootdPath`, and the path of your output folder as `treeBaseDir`. You should end up with something like:
```
'xrootdPath': 'root://eoshome-g.cern.ch/',
'treeBaseDir': '/eos/user/g/gpizzati/nanoAOD/postProc',
``` 
<!-- I want to send output files in my eos folder, so I changed content of the key 'cern', you can look at here:

`/afs/cern.ch/work/j/jixiao/public/forElena/framework/Sites_cfg.py` -->

### Second step
To make the framework input root files in your eos (I suggest to put your private nanoAOD in your eos folder), 
then you need to change PostProcMaker.py:

We want the framework to know the right redirector to use, it should be the same url you used above.
Change this line to something like: `self._aaaXrootd = 'root://eoshome-g.cern.ch/'` 

### Third step
Add your samples in the file samples/Autumn18_102X_nAODv7.py. Create a new key-value pair in the `Samples` dictionary and specify in srmPrefix your eos url and in paths the path of your input nanoAOD (i.e. the ones you generated in FULL-SIM)
 <!-- if you put your private nanoAOD root files in eos, here is an example: -->
Here's an example:
```
Samples['hmn_m50']={'srmPrefix':'root://eoshome-g.cern.ch/',
                    'paths' :['/eos/user/g/gpizzati/nanoAOD/Zjj_SM_5f']}
```

<!-- We need to add 'srmPrefix', and eos folder, it's different from official samples.

If it does not work, it's worth trying with: 
`Samples['WZeu_SM']={'srmPrefix':'root://eosuser.cern.ch/','paths' :['/eos/user/e/evernazz/nanoAOD_ntuple/WZeu_SM']}` -->

 ### Fourth
Add your samples cross sections in samples/samplesCrossSections2018.py.
You should add a key-value pair in the samples dictionary.
e.g. : 
`samples['EWKZ_2Jets_No_Higgs'].extend( ['xsec=1.0',     'kfact=1.000',   'ref=Z' ])`
The xs used can be the one given by MG at parton level. 

If you used [D6EFTStudies](https://github.com/UniMiBAnalyses/D6EFTStudies), you will find it in the file `RESULTS_FOLDER/read_03_input.cfg` after the postProcess step.

<!-- ```
cp /afs/cern.ch/work/j/jixiao/public/forElena/framework/PostProcMaker.py ./
cp /afs/cern.ch/work/j/jixiao/public/forElena/framework/FatJetCorrHelper.py ./
cp /afs/cern.ch/work/j/jixiao/public/forElena/framework/Steps_cfg.py ./
``` -->
Finally you can set voms proxy with: `voms-proxy-init -voms cms -valid 192:00`,
 and run the commands below. 
 
 *Remember to run grid before all of the commands below if your proxy expires*



# Final commands

1. `mkPostProc.py -p Autumn18_102X_nAODv7_Full2018v7 -s MCl1loose2018v7 -b -Q workday -T YOUR_SAMPLE_NAME`


2. `mkPostProc.py -p Autumn18_102X_nAODv7_Full2018v7 -s MCCorr2018v7 -i MCl1loose2018v7 -b -Q workday -T YOUR_SAMPLE_NAME`

3. `mkPostProc.py -p Autumn18_102X_nAODv7_Full2018v7 -s l2loose -i MCl1loose2018v7__MCCorr2018v7 -b -Q workday -T YOUR_SAMPLE_NAME`

If the last step isn't working, please edit the following files in 
`LatinoAnalysis/NanoGardener/python/data/DYSFmva/2018_alt/`:
```
TMVAClassification_PyKeras_2018_0j.weights.xml
TMVAClassification_PyKeras_2018_1j.weights.xml
TMVAClassification_PyKeras_2018_2j.weights.xml
TMVAClassification_PyKeras_2018_VBF.weights.xml
TMVAClassification_PyKeras_2018_VH.weights.xml
```
A simple sed should fix the problem (supposing you're in CMSSW/src)

<!-- `sed -i 's@<Option name="FilenameTrainedModel" modified="No">.*@<Option name="FilenameTrainedModel" modified="No">'`pwd`'/LatinoAnalysis/NanoGardener/python/data/DYSFmva/2018_alt/TrainedModel_PyKeras_2018_0j.h5</Option>@g' LatinoAnalysis/NanoGardener/python/data/DYSFmva/2018_alt/TMVAClassification_PyKeras_2018_0j.weights.xml` -->

```
array=( 0j 1j 2j VBF VH )
for i in "${array[@]}"
do
	sed -i 's@<Option name="FilenameTrainedModel" modified="No">.*@<Option name="FilenameTrainedModel" modified="No">'`pwd`'/LatinoAnalysis/NanoGardener/python/data/DYSFmva/2018_alt/TrainedModel_PyKeras_2018_'${i}'.h5</Option>@g' LatinoAnalysis/NanoGardener/python/data/DYSFmva/2018_alt/TMVAClassification_PyKeras_2018_${i}.weights.xml
done
```

<!-- 
The same command should be repeated for the last two files

`sed -i 's@<Option name="FilenameTrainedModel" modified="No">.*@<Option name="FilenameTrainedModel" modified="No">'`pwd`'/LatinoAnalysis/NanoGardener/python/data/DYSFmva/2018_alt/TrainedModel_PyKeras_2018_0j.h5</Option>@g' TMVAClassification_PyKeras_2018_VBF.weights.xml`

`sed -i 's@<Option name="FilenameTrainedModel" modified="No">.*@<Option name="FilenameTrainedModel" modified="No">'`pwd`'/LatinoAnalysis/NanoGardener/python/data/DYSFmva/2018_alt/TrainedModel_PyKeras_2018_0j.h5</Option>@g' TMVAClassification_PyKeras_2018_VH.weights.xml`
 -->



<!-- bisogna far riferimento al proprio path: afs/cern.ch/user/e/evernazz/CMSSW_10_6_4/src/LatinoAnalysis/NanoGardener/python/data/DYSFmva/2018_alt/TrainedModel_PyKeras_2018_2j.h5 -->


4. `mkPostProc.py -p Autumn18_102X_nAODv7_Full2018v7 -s l2tightOR2018v7 -i MCl1loose2018v7__MCCorr2018v7__l2loose -b -Q workday -T YOUR_SAMPLE_NAME`
