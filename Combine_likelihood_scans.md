- [Documentation about likelihood scans](http://cms-analysis.github.io/HiggsAnalysis-CombinedLimit/part3/commonstatsmethods/#likelihood-fits-and-scans)
- [How to breakdown uncertainties](https://indico.cern.ch/event/976099/contributions/4138475/attachments/2163619/3651163/UncertBreakdown_AdeWit.pdf)

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
