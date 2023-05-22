# Use Jupyter notebook from a remote machine

## Setup your `.ssh/config` file to connect to you remote machine
```
### Mib
Host    cerbero
        HostName cerbero.mib.infn.it
        # Specify the re ur local one 
        User gpizzati
        Compression yes
        # Use SSHv2 only 
        Protocol 2
        # Forward you SSH key agent so that it can be used on further hops
        ControlMaster auto
        ControlPath ~/.ssh/%r@%h:%p
        ForwardAgent yes
        # In case there is kerberos configured locally
        #GSSAPITrustDns yes
        GSSAPIAuthentication yes
        GSSAPIDelegateCredentials yes
```
If your machine needs a proxy jump you can then write

```
Host    hercules
        HostName hercules
        # Specify the re ur local one 
        User gpizzati
        Compression yes
        # Use SSHv2 only 
        Protocol 2
        # Forward you SSH key agent so that it can be used on further hops
        ControlMaster auto
        ControlPath ~/.ssh/%r@%h:%p
        ForwardAgent yes
        # For X11
        ForwardX11 yes
        ForwardX11Trusted yes
        # In case there is kerberos configured locally
        #GSSAPITrustDns yes
        GSSAPIAuthentication yes
        GSSAPIDelegateCredentials yes
        ProxyJump cerbero

``` 
and simply login with:

`ssh hercules` 

---

## On the remote machine run the jupyter notebook
You may want to source the right environment such as:

`source /cvmfs/sft.cern.ch/lcg/views/LCG_103/x86_64-centos7-gcc11-opt/setup.sh` 

and then run the command:

`jupyter notebook`

from the output look for the link with localhost and take note of the port `http://localhost:PORT/token?....`

---

## Open port to remote machine
You can open the port that was taken by jupyter and expose it to your lapton as 8888 or whatever port is free on your pc:

`ssh hercules -NL PORT1:localhost:PORT` 

---

## Open the link jupyter gave you on your browser

Open `http://localhost:PORT1/token?....` with the port you opened 

