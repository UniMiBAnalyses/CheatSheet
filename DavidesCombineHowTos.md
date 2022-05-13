# Combine HowTos

- Site web combine [http://cms-analysis.github.io/HiggsAnalysis-CombinedLimit/](http://cms-analysis.github.io/HiggsAnalysis-CombinedLimit/)

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
`text2workspace.py combined.txt -o combined.roo`

- Fit con likelihood scan con Asimov dataset
`combine -M FitDiagnostics -t -1 --expectSignal=1 combined.root &> logFit.tx` 

- Fit con likelihood scan con Asimov but using the post-fit values for nuisances
`combine -M FitDiagnostics -t -1 --expectSignal=1 --toysFrequentist combined.root &> logFit.txt`

See Likelihood scan item for more instructions.