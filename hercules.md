# Usage of the Milano-Bicocca Hercules cluster

## get an account

  * usually an account is made for any student and researcher at the moment of registration
  * if you do not have an account, ask Paolo Dini for one, and if you're a student
    ask your supervisor to provide you with her/his request approval

## login

  * the access server is named ```hercules.mib.infn.it```
  * the server is not accessible from outside the INFN Milano-Bicocca network, 
    therefore one should first connect to ```cerbero```,
    and then from there to ```hercules```:
```
ssh username@cerbero.mib.infn.it
ssh username@hercules.mib.infn.it
```

## Connect to CERN AFS and eos

Run the following commands from within hercules (better save them in bash or setup script)

```
export KRB5CCNAME=/gwpool/users/<hercules_username>/krb5cc_`id -u <hercules_username>`
kinit
eosfusebind -g
aklog
```

If your hercules username does not match you lxplus username:

```
export KRB5CCNAME=/gwpool/users/<hercules_username>/krb5cc_`id -u <hercules_username>`
kinit -f <lxplus_username>@CERN.CH
eosfusebind -g
aklog
```

## Run Latinos on Hercules

Latinos won't work out of the box. A branch was made to let latinos work on hercules:
https://github.com/UniMiBAnalyses/LatinoAnalysis/tree/VBS_skim_giacomo

Details are in the README of the VBS_skim_giacomo branch.

```git clone --branch VBS_skim_giacomo git@github.com:UniMiBAnalyses/LatinoAnalysis.git```


## CMSSW configuration


## use HTCondor


