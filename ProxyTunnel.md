How a proxy tunnel work:

When you connect with **SSH** you create an encrypted tunnel from your computer to a remote computer.

For the connection to Hercules a double step is used:

First you connect to Virgilio (ssh UserName@virgilio.mib.infn.it), then you connect to another remote computer (from virgilio to hercules), creating another tunnel. This is necessary for the safety of the second computer.
Now, with the istructions in the link below you can configure your computer in order to do this double step with one command == **proxy tunnel**

**ProxyCommand ssh virgilio nc %h %p**: tell to SSH to connect to hercules through the host %h (virgilio) and using the port %p

Link to istructions: https://docs.google.com/document/d/15__C64kTrdyaUplczE0hLkhrIZWsNuoeFGUsttCVsR0/edit?usp=sharing
