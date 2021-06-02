# How to use a _screen_ shell in lxplus

Access an lxplus (remember the machine number), e.g.

    [ribrusa@lxplus751 ~]$

751 is the machine number.

In order to open a new _screen_ session, just type

    screen

In order to view if there are active _screen_ sessions

    screen -r

In case there are no active sessions you will see _There is no screen to be resumed_, if there is one active session, you will be addresed to it, finally if there are more than one active session (not reccomended) you will see something like

    There are several suitable screens on:
	    13929.pts-32.lxplus751	(Detached)
	    5839.pts-32.lxplus751	(Detached)
    Type "screen [-d] -r [pid.]tty.host" to resume one of them.

You can access one particular active session by typing

    screen -r 13929.pts-32.lxplus751

In order to exit:

* Simply leave (without terminating the session): ctrl+A+D
* Kill the _screen_ session: ctrl+D

If you leave lxplus and you want to access again a _screen_ active session, you have to access the same lxplus (751 in this example).

Activate the cms environment:
   
   `source /cvmfs/cms.cern.ch/cmsset_default.sh`

Now you should be able to execute `cmsenv`and all other cms alias commands from within the screen session.

Warning: the _screen_ shell could result a limited one, but workarounds are available. For example if _cmsenv_ does not work, you can use

    eval `scramv1 runtime -sh`


