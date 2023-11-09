# Guide for Remote Access with SSH in Visual Studio Code

## 1. Install Visual Studio Code

You can install Visual Studio Code using the following commands:


    sudo snap install --classic code


## 2. Install the "Remote - SSH" Extension

1. Open Visual Studio Code.
2. Go to the left sidebar and click on the Extensions icon (or press `Ctrl+Shift+X`).
3. Search for "Remote - SSH" and install the extension provided by Microsoft.


## 3. Connect to the Remote Server

1. Open the command menu (`Ctrl+Shift+P`) and search for the "Remote-SSH: Connect to Host..." command
2. Go on `Add New SSH Host` and add your SSH server as `ssh nome_utente@hercules.mib.infn.it` and `ssh nome_utente@hercules.mib.infn.it`

## 4. Open the remote server

1. Go the left sidebar and click on "Remote Explorer"
2. Open the "REMOTES (TUNNELS/SSH)" section and than the "SSH" section. You will found the option `hercules.mib.infn.it` and `hercules.mib.infn.it`
3. Click to connect: you will be prompted to enter the password for your server if you haven't configured SSH keys.

After the connection, you can work directly on the remote server.

## 6. Disconnect from the Remote Server

When you're done working, you can disconnect from the remote server by clicking on the icon in the bottom-left corner of Visual Studio Code and selecting "Disconnect Remote."

Now you're ready to start working on your remote server using Visual Studio Code!

   

