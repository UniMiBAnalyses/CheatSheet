# Combine HowTos

- **Site web combine** [http://cms-analysis.github.io/HiggsAnalysis-CombinedLimit/](http://cms-analysis.github.io/HiggsAnalysis-CombinedLimit/)

- Tutorials: [https://indico.cern.ch/event/577649/?filterActive=1&showDate=all&showSession=2](https://indico.cern.ch/event/577649/?filterActive=1&showDate=all&showSession=2)

- PhysicsModel: [https://indico.cern.ch/event/577649/contributions/2388732/attachments/1380305/2100706/HComb_PhysicsModels_Nov30.pdf](https://indico.cern.ch/event/577649/contributions/2388732/attachments/1380305/2100706/HComb_PhysicsModels_Nov30.pdf)

- Twiki utile per combine [https://twiki.cern.ch/twiki/bin/viewauth/CMS/HWWCombineTools](https://twiki.cern.ch/twiki/bin/viewauth/CMS/HWWCombineTools)

- CMSDAS 2019 HWW combine [https://twiki.cern.ch/twiki/bin/view/CMS/SWGuideCMSDataAnalysisSchoolBeijing2019LongHWW](https://twiki.cern.ch/twiki/bin/view/CMS/SWGuideCMSDataAnalysisSchoolBeijing2019LongHWW)

- Guide about several combine methods: [https://cms-analysis.github.io/HiggsAnalysis-CombinedLimit/part3/commonstatsmethods](https://cms-analysis.github.io/HiggsAnalysis-CombinedLimit/part3/commonstatsmethods)

- Combine options: [https://cms-analysis.github.io/HiggsAnalysis-CombinedLimit/part3/runningthetool/#common-command-line-options](https://cms-analysis.github.io/HiggsAnalysis-CombinedLimit/part3/runningthetool/#common-command-line-options)

- HIG PAS pre-approval combine checks: [https://twiki.cern.ch/twiki/bin/viewauth/CMS/HiggsWG/HiggsPAGPreapprovalChecks](https://twiki.cern.ch/twiki/bin/viewauth/CMS/HiggsWG/HiggsPAGPreapprovalChecks)

- Goodness Of Fit test: [https://cms-analysis.github.io/HiggsAnalysis-CombinedLimit/part3/commonstatsmethods/#goodness-of-fit-tests](https://cms-analysis.github.io/HiggsAnalysis-CombinedLimit/part3/commonstatsmethods/#goodness-of-fit-tests)

- HComb 2019 hands-on: [https://twiki.cern.ch/twiki/bin/viewauth/CMS/HiggsWG/HCombExercise](https://twiki.cern.ch/twiki/bin/viewauth/CMS/HiggsWG/HCombExercise)

- New post-fit tools: [https://indico.cern.ch/event/971994/contributions/4094027/attachments/2146209/3617533/PAT_stattools_AdeWit_1911.pdf](https://indico.cern.ch/event/971994/contributions/4094027/attachments/2146209/3617533/PAT_stattools_AdeWit_1911.pdf)

- HWW Combine tutorial [https://twiki.cern.ch/twiki/bin/viewauth/CMS/HWWCombineTools](https://twiki.cern.ch/twiki/bin/viewauth/CMS/HWWCombineTools)

- Andrea Massironi and Latinos tools:

    - [https://github.com/latinos/PlayWithDatacards](https://github.com/latinos/PlayWithDatacards)
    - [https://github.com/amassiro/ModificationDatacards](https://github.com/amassiro/ModificationDatacards)
    - [https://github.com/latinos/LatinoCombineTools/tree/master/Tools](https://github.com/latinos/LatinoCombineTools/tree/master/Tools)
    - [https://github.com/latinos/LatinoAnalysis/tree/master/ShapeAnalysis/test/draw](https://github.com/latinos/LatinoAnalysis/tree/master/ShapeAnalysis/test/draw)
    - Statistical scripts: [https://github.com/amassiro/StatisticalTool](https://github.com/amassiro/StatisticalTool)
    - Impact plots without correlation: [https://github.com/latinos/LatinoCombineTools/tree/master/Impact](https://github.com/latinos/LatinoCombineTools/tree/master/Impact)
    - Scale one samples: [https://github.com/amassiro/ModificationDatacards#scale-one-sample-by-a-factor](https://github.com/amassiro/ModificationDatacards#scale-one-sample-by-a-factor)
    - Grid scan for nuisances: [https://github.com/amassiro/StatisticalTool/tree/master/GridNuisances](https://github.com/amassiro/StatisticalTool/tree/master/GridNuisances)
- `--toysFrequentist` explanation: [https://hypernews.cern.ch/HyperNews/CMS/get/higgs-combination/895/1.html](https://hypernews.cern.ch/HyperNews/CMS/get/higgs-combination/895/1.html)

- Postfit distributions [http://cms-analysis.github.io/CombineHarvester/post-fit-shapes-ws.html](http://cms-analysis.github.io/CombineHarvester/post-fit-shapes-ws.html)

- Resampling in FitDiagnostic to numpy: [https://hypernews.cern.ch/HyperNews/CMS/get/higgs-combination/1493/3.html](https://hypernews.cern.ch/HyperNews/CMS/get/higgs-combination/1493/3.html)

- Validate the datacards: [http://cms-analysis.github.io/HiggsAnalysis-CombinedLimit/part3/validation/](http://cms-analysis.github.io/HiggsAnalysis-CombinedLimit/part3/validation/)

Combine è legato alla versione di CMSSW perchè di base usa root. Noi usiamo 10_2_13.




# Fit details

- FitDiagnostic details and options: [https://github.com/cms-analysis/HiggsAnalysis-CombinedLimit/wiki/nonstandard#fit-parameter-uncertainties](https://github.com/cms-analysis/HiggsAnalysis-CombinedLimit/wiki/nonstandard#fit-parameter-uncertainties)
- Minimizer options [https://github.com/cms-analysis/HiggsAnalysis-CombinedLimit/wiki/runningthetool#generic-minimizer-options-](https://github.com/cms-analysis/HiggsAnalysis-CombinedLimit/wiki/runningthetool#generic-minimizer-options-)
- Save normalizations: [script](https://github.com/cms-analysis/HiggsAnalysis-CombinedLimit/blob/81x-root606/test/mlfitNormsToText.py)
- Post-fit uncertainties explained [HN](https://hypernews.cern.ch/HyperNews/CMS/get/higgs-combination/995.html)
- Debugging fits: [https://indico.cern.ch/event/976099/contributions/4138476/attachments/2163625/3651175/CombineTutorial-2020-debugging.pdf](https://indico.cern.ch/event/976099/contributions/4138476/attachments/2163625/3651175/CombineTutorial-2020-debugging.pdf)
# Comandi
- Creare la datacard:

`text2workspace.py combined.txt -o combined.root`

- Fit con likelihood scan con Asimov dataset

`combine -M FitDiagnostics -t -1 --expectSignal=1 combined.root &> logFit.txt` 

- Fit con likelihood scan con Asimov but using the post-fit values for nuisances

`combine -M FitDiagnostics -t -1 --expectSignal=1 --toysFrequentist combined.root &> logFit.txt`

See Likelihood scan item for more instructions.

- [Documentation about likelihood scans](http://cms-analysis.github.io/HiggsAnalysis-CombinedLimit/part3/commonstatsmethods/#likelihood-fits-and-scans)
- [How to breakdown uncertainties](https://indico.cern.ch/event/976099/contributions/4138475/attachments/2163619/3651163/UncertBreakdown_AdeWit.pdf)

# Some useful commands


### Likelihood scan with freezing
1. First of all perform a initial fit and save the snapshot

```combine -M MultiDimFit combined.root  -n .snapshot --rMin 0 --rMax 2 --saveWorkspace -t -1 --expectSignal=1 --robustFit=1 --toysFreq```

2. Perform a likelihood scan without freezing any parameter

```combine -M MultiDimFit combined.root  -n .scan  --rMin 0 --rMax 2 --saveWorkspace -t -1 --expectSignal=1 --robustFit=1 --toysFreq --algo grid --points 30```

3. Freeze all nuisances and perform the scan loading best fit values from snapshot

```combine -M MultiDimFit combined.snapshot.root   -n .freezeAll  --rMin 0 --rMax 2  -t -1 --expectSignal=1 --robustFit=1 --toysFreq  --algo grid --points 30  --freezeParameters "rgx{.*}"  --snapshotName MultiDimFit```

4. Plot the two plots:

```python $COMBINE_TOOLS/plot1DScan.py initial_scan.root --others 'freezed_scan.root:FreezeAll:2' -o freeze_second_attempt --breakdown Syst,Stat```

![](https://dvalsecc.web.cern.ch/dvalsecc/VBSPlots/FullRun2/fits_results/preliminary_fit_fullrun2/fit_diagnostic/2018_boosted_likelihoodscan.png)


###  2D likelihood scan
The following commad performs a scan on the signal strength and a nuisance parameters with a MC asimov dataset
```bash
combine   -d workspace.root  \ 
-M MultiDimFit  \
--redefineSignalPOIs QCDscale_wjets,r   \
--setParameterRanges QCDscale_wjets=-3,3:r=0.5,1.5  \
 -t -1 --expectSignal=1 \
--algo grid -m 125 \
--points 1000
```

The combineTool can be used to speed up the process
```bash
combineTool.py -M MultiDimFit  -d workspace.root \
 --redefineSignalPOIs QCDscale_wjets,r  \
 --setParameterRanges r=0,2:QCDscale_wjets=-3,3 \
-t -1 --expectSignal=1  -n "mu_QCDscaleWjets" \
-m 125 --algo grid --points 1000 \
--job-mod condor --task-name qcdscale_mu --split-point 10
```

### Scan on Likelihood saving all the nuisances profiling mu
Perform a likelihood scan on a parameter but save all the values of the profiles nuisances
```bash
combineTool.py -d workspace.root  -M MultiDimFit    \
 --algo=grid   --X-rtd OPTIMIZE_BOUNDS=0  --rMin 0.5 --rMax 1.5 \
--saveSpecifiedNuis all   -n "name"   \
--points 400    --job-mode condor --task-name task-name --split-points 1 
--trackParameters "rgx{.*_norm_.*}"
```
be careful to include `-t -1 --setParameters r=1` if you want to fit the asimov dataset and not the data.

In order to track also the rate params another option needs to be added with a regex
```bash
--trackParameters "rgx{.*_norm_.*}"

```

To plot the 2D points use the script `plot2Dscan_params`:

### Scan on Likelihood profiling one nuisance parameter
Perform scan on NUisance parameter saving the value of all the others nuisances and `r`. Useful to check the correlations. Using the `--redefineSignalPOI` all the constraint terms on the nuisance are removed and not considered in the fits.  If the constraints need to be included use the option `--parameters nuisance` to select the POI for the scan.

```bash
combineTool.py -d workspace.root -M MultiDimFit  --algo=grid \
 --redefineSignalPOI  NUISANCE --setParameterRanges r=-2,3:NUISANCE=-1.2,1.2\
 --setParameters r=1  -n "PSscan" --points N --saveSpecifiedNuis all\
 --trackParameters "rgx{.*},r"  -t -1 \
--job-mode condor --task-name task-name --split-points 1 
```
The `--setParameters r=1` is needed to build the asimov dataset
