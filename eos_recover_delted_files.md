# EOS Recycle bin

In case a rm -rf was wrongfully issued upon a eos directory it is possible to recover all the deleted files.
The EOS recycle bin allows to define a FIFO policy for delayed file deletion.
The recycling bin is time-based and volume based and performs final deletion after a configurable time delay. The volume in the recycle bin is limited using project quota. *If the recycle bin is full no further deletion is possible and deletions fails until enough space is available*.

The owner of a deleted file or subtree deletion can restore files into the original location from the recycle bin if he has the required quota.

The recycling bin is time-based and volume based and performs final deletion after a configurable time delay. The volume in the recycle bin is limited using project quota. *If the recycle bin is full no further deletion is possible and deletions fails until enough space is available*

```
EOS Console [root://eosuser.cern.ch] |/eos/user/g/gboldrin/www/> recycle
# pre-configuring default route to /eos/user/g/gboldrin/
# -use $EOSHOME variable to override
# ___________________________________________________________________________________________________________________________
# used 1.03 PB out of 1.50 PB (68.39% volume / 50.60% inodes used) Object-Lifetime 15552000 [s] Keep-Ratio 0.20
# ___________________________________________________________________________________________________________________________
```

See bin content 

```
EOS Console [root://eosuser.cern.ch] |/eos/user/g/gboldrin/www/> recycle ls 2021/09/21
# pre-configuring default route to /eos/user/g/gboldrin/
# -use $EOSHOME variable to override
# Deletion Time            UID      GID      SIZE         TYPE          RESTORE-KEY          RESTORE-PATH                                                    
# ==============================================================================================================================
Tue Sep 21 11:07:29 2021   gboldrin def-cg   34675108     recursive-dir pxid:000000000576cce3 /eos/user/g/gboldrin/www/2DInspect_2/OSWW_noQuad                
Tue Sep 21 10:01:18 2021   gboldrin def-cg   35564266     recursive-dir pxid:00000000057a97c4 /eos/user/g/gboldrin/www/2DInspect_2/SSWW_noQuad                
Tue Sep 21 10:54:30 2021   gboldrin def-cg   35564266     recursive-dir pxid:00000000057be2c8 /eos/user/g/gboldrin/www/2DInspect_2/SSWW_noQuad                
Tue Sep 21 11:07:33 2021   gboldrin def-cg   35564266     recursive-dir pxid:00000000057bfbb5 /eos/user/g/gboldrin/www/2DInspect_2/SSWW_noQuad                
Tue Sep 21 11:07:38 2021   gboldrin def-cg   35863755     recursive-dir pxid:000000000554fda9 /eos/user/g/gboldrin/www/2DInspect_2/WZ_noQuad                  
Tue Sep 21 11:07:42 2021   gboldrin def-cg   41288067     recursive-dir pxid:00000000057a62af /eos/user/g/gboldrin/www/2DInspect_2/ZZ_noQuad                  
Tue Sep 21 11:07:46 2021   gboldrin def-cg   12483555     recursive-dir pxid:00000000057a4491 /eos/user/g/gboldrin/www/2DInspect_2/inWW_noQuad                
Tue Sep 21 12:04:01 2021   gboldrin def-cg   6287213      recursive-dir pxid:0000000005752ce0 /eos/user/g/gboldrin/www/New/OSWW_noQuad                        
Tue Sep 21 12:04:36 2021   gboldrin def-cg   1718152      recursive-dir pxid:0000000005752cb7 /eos/user/g/gboldrin/www/New/inWW_noQuad                        
Tue Sep 21 11:08:29 2021   gboldrin def-cg   5825398      recursive-dir pxid:00000000057a0334 /eos/user/g/gboldrin/www/OSWW                                   
Tue Sep 21 11:51:34 2021   gboldrin def-cg   6022177      recursive-dir pxid:00000000057c1d0f /eos/user/g/gboldrin/www/OSWW_noQuad                            
Tue Sep 21 11:08:08 2021   gboldrin def-cg   42131292     recursive-dir pxid:00000000057a36f7 /eos/user/g/gboldrin/www/ZZ_2D_noQuad                           
Tue Sep 21 11:23:24 2021   gboldrin def-cg   1566563      recursive-dir pxid:00000000057c09bb /eos/user/g/gboldrin/www/inWW_noQuad                            
Tue Sep 21 11:51:39 2021   gboldrin def-cg   1569279      recursive-dir pxid:00000000057c160e /eos/user/g/gboldrin/www/inWW_noQuad 
```

Restore a file with the restore command and the "RESTORE-KEY"

```

EOS Console [root://eosuser.cern.ch] |/eos/user/g/gboldrin/www/> recycle restore pxid:000000000576cce3
# pre-configuring default route to /eos/user/g/gboldrin/
# -use $EOSHOME variable to override
success: restored path=/eos/user/g/gboldrin/www/2DInspect_2/OSWW_noQuad
EOS Console [root://eosuser.cern.ch] |/eos/user/g/gboldrin/www/> ls 2DInspect_2/OSWW_noQuad
cHDD_cHW_deltaetajj.png
cHDD_cHW_deltaphijj.png
cHDD_cHW_etaj1.png
cHDD_cHW_etaj2.png
cHDD_cHW_etal1.png
...
```

# Resources
- https://twiki.cern.ch/twiki/bin/view/EOS/RecoverDeletedData
- https://twiki.cern.ch/twiki/bin/view/EOS/EOSLostFiles (old)
