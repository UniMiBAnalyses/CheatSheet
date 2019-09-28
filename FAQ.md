-Where do I begin?

    A-You have to configurate your account on hercules! Follow the instrunctions here:
    https://docs.google.com/presentation/d/1-Hb5WXXzh-DvXmM1YBS-0j-YYFYemwJAPaaYzfXhlXw/edit#slide=id.g4e61244e2c_1_0
    All the work will have to be done meanwhile you are conncted to the cluster!

Q-How do I move files and directory from my pc to hercules?      

    A-With the command scp, you will have to create an "alias" because the connection to hercules is mediated by virglio. All the instruction are here:
    https://github.com/UniMiBAnalyses/CheatSheet/blob/master/ProxyTunnel.md



Q-How to orient myself in github?

    A-Most of the page of github are people's page that contain their code, the structure of that page is similar.
    In the README.md most of the latinos(group) write a guide, you can follow that for understand what to do.
    For example: https://github.com/UniMiBAnalyses/PlotsConfigurations/tree/master/Configurations/VBSWWOS

Q-What if  mkBatch.py --status doesn't function?

    A- It's normal, just use the command qstat.

Q-Why do mkSphapes.py doesn't function?

    A-There could be many reason, you can check if in the file samples.py, at the end of every line 'getsample', there is for last argument 'True'.

Q-What is the difference between mkShapes.py and mkPlot.py?

    A- The first create a lot of histograms for every events, the second put them togheter and make them nicer.

Q-What does the variables mean?

    A-check this page:
    https://github.com/latinos/LatinoAnalysis/blob/master/Gardener/python/variables/WWVar.C
    and in general in the folder
    https://github.com/latinos/LatinoAnalysis/blob/master/Gardener/python/variables/
    
Q-Something is not clear and I don't know where it is defined

    A-try to use the "search or jump to ..." field on github (top left, next to the cat logo) while being in the link
    https://github.com/latinos/LatinoAnalysis

Q-How to use EasyDescription to see what mkShapes will read from your configuration?
    
    A-you just need to use easyDescription.py as explained in this link
    https://github.com/UniMiBAnalyses/CheatSheet/blob/master/LatinoPlots.md
    
Q-How do I display an image on Hercules?
    
    A-You can use the command 'display'. Be sure you connected both to Virgilio and Hercules with the '-X' option (ssh -X). 
    If you setup a proxy tunnel to automatically connect to Hercules, be sure that the "forward" fields in the
    configuration file are set to "yes". If you face problems, exit Hercules and use the command 'killall ssh', then try again.
    
Q-How to retrieve DAS sample names from 'latino' ones?

    A-You can refer to this Python dictionary: https://github.com/latinos/LatinoTrees/blob/master/AnalysisStep/test/crab/samples/samples_summer16_Feb2017.py
    The 'latino' sample name is the key of the samples dictionary. The value is a list and its first item is the DAS name.
