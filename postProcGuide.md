# Postprocessing guide for [LatinoAnalysis NanoGardener](https://github.com/latinos/LatinoAnalysis/tree/master/NanoGardener)

This guide is divided in two sections. In the first one the reader is instructed on how to process centrally produced nanoAOD, enabling the processing of virtually any sample for your analysis (in particular this is extremely useful for most common background processes such as DY, multijet QCD, top induced processes etc.. ). Bear in mind that the Latinos group already processed plenty of samples, so before starting the postprocessing of a sample, check the following files and see wether your sample has been already processed:
- 2016: https://github.com/latinos/LatinoAnalysis/blob/76e7c4b93aa5f056c92440d4e8d24e7de749c8fe/NanoGardener/python/framework/samples/Summer16_102X_nAODv7.py
- 2017: https://github.com/latinos/LatinoAnalysis/blob/76e7c4b93aa5f056c92440d4e8d24e7de749c8fe/NanoGardener/python/framework/samples/fall17_102X_nAODv7.py
- 2018: https://github.com/latinos/LatinoAnalysis/blob/76e7c4b93aa5f056c92440d4e8d24e7de749c8fe/NanoGardener/python/framework/samples/Autumn18_102X_nAODv7.py

## Process centrally produced nanoAOD

Suppose you started a new and very fancy analysis. You realize that somehow one of the needed background is not available in the Latinos central folder. First thing you need to check wether centrally produced nanoAOD do exist (which are "vanilla nanoAOD", before the Latino post-processing). To do so you might want to consult the CMS Data Aggregation System: https://cmsweb.cern.ch/das/request?view=list&limit=50&instance=prod%2Fglobal&input=dataset%3D%2FDYJetsToLL_0J*%2F*NanoAODv7*102X*%2FNANOAODSIM

Pay attention to the syntax you use to query datasets. The first entry `DYJetsToLL_0J*` is just the dataset name, followed by the MC Tune `TuneCP5` for underlying events, the COM energy `13TeV`, the hard process MC generator `amcatnlo`, the parton-jet marging algorithm `FXFX` and the parton shower `pythia8`. The second entry is the central production camapign `RunIIAutumn18NanoAODv7-Nano02Apr2020_102X` which tells you the date of the campaign, the nanoAOD version for the campaign `NanoAODv7` and the CMS version used for the processing `102X`. It is important that the samples you select are processed with version 7 of the nanoAOD `NanoAODv7` as the Latino Frameworks only works with this version. The last line is the global tag and version (detector geometry etc etc) used for the campaign `upgrade2018_realistic_v21-v1`. Lastly, and this is important, the dataset type you want in our case it is mandatory the `NANOAODSIM` step (there are many others, slide 26 here https://conference.ippp.dur.ac.uk/event/704/attachments/3462/3813/CMS_data_mc_IPPP.pdf ).

Once you find the dataset you want to process with Latinos framework e.g. `/DYJetsToLL_0J_TuneCP5_13TeV-amcatnloFXFX-pythia8/RunIIAutumn18NanoAODv7-Nano02Apr2020_102X_upgrade2018_realistic_v21-v1/NANOAODSIM` you have to edit some Latinos files in order for xrdcp to take this root filles distributed over the various Tier2, issue the processing, and copy the output on your personal eos (by default it will try to copy the output to `/eos/cms/store/group/phys_higgs/cmshww/amassiro/HWWNano/` which is a special directory with limited write access.

In `Sites_cfg.py` line 16 (https://github.com/latinos/LatinoAnalysis/blob/76e7c4b93aa5f056c92440d4e8d24e7de749c8fe/NanoGardener/python/framework/Sites_cfg.py#L16) modify the dict entry as follows:

``` 
  'cern' : {
              'lsCmd'       : 'ls' ,
              'mkDir'       : True ,
              'xrootdPath'  : 'root://eosuser.cern.ch/' ,
            #  'treeBaseDir' : '/eos/cms/store/group/phys_higgs/cmshww/amassiro/HWWNano/' ,
              'treeBaseDir' : '/eos/user/g/gboldrin/nanoLatino/' ,
              'treeBaseDirOut' : '/eos/user/g/gboldrin/nanoLatino/' ,
              'batchQueues' : ['8nh','1nd','2nd','1nw'],
              'slc_ver'     : 7
           } ,
```

where the entries `treeBaseDir`and `treeBaseDirOut` should point to an existing folder on your personal eos. Secondly uncomment the following line https://github.com/latinos/LatinoAnalysis/blob/76e7c4b93aa5f056c92440d4e8d24e7de749c8fe/NanoGardener/python/framework/PostProcMaker.py#L32

Now you just need to add your sample to the samples configuration (https://github.com/latinos/LatinoAnalysis/blob/76e7c4b93aa5f056c92440d4e8d24e7de749c8fe/NanoGardener/python/framework/samples/Autumn18_102X_nAODv7.py). The order is not important. Just add an entry where the key `DYJetsToLL_0J` in this example is arbitrary:
``` 
Samples['DYJetsToLL_0J'] = {'nanoAOD' : '/DYJetsToLL_0J_TuneCP5_13TeV-amcatnloFXFX-pythia8/RunIIAutumn18NanoAODv7-Nano02Apr2020_102X_upgrade2018_realistic_v21-v1/NANOAODSIM'}
```

Now you can run the first step of the post-processing as follows:

```
mkPostProc.py -p Autumn18_102X_nAODv7_Full2018v7 -b -s MCl1loose2018v7 -Q tomorrow -T DYJetsToLL_0J 
```

Where no `-i` step should be specified as we are starting from scratch. In order to further process this sample after this step is finished some changes are needed because we would want to take the output of the `MCl1loose2018v7` step which is now on our eos space. In order to do such please read the next chapter.


## Process privately produced nanoAOD


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
