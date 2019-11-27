# Guide for SSH on Lxplus

## 0. Access Lxplus

    ssh -x username@lxplus.cern.ch

## 1. Create an SSH key

Start ssh agent:


    eval "$(ssh-agent -s)"
    ssh-add -l

create an ssh key:


    ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

When asked for the key location enter:

    
    /afs/cern.ch/user/<U>/<UserName>/.ssh/id_rsa

Fix permissions:


    chmod 400 <key_file_location>

Choose a password and add the key:


    ssh-add <key_file_location>


## 2. Add the key to SSH-Keys in your GitHub account 

From https://github.com/ go to:

settings -> SSH and GPH keys -> new SSH keys 

Paste the content of id_rsa.pub

## 3. Add a new host to ssh config

Following the instructions here:

https://medium.com/@czarpino/how-to-tell-git-which-ssh-key-to-use-c8574fb243fd

open ~/.ssh/config and configure a new host in the following way:


    # ~/.ssh/config
    Host repo_<name>
        Hostname github.com
        User git
        IdentityFile ~/.ssh/private_key_name

where private_key_name corresponds to the private key you created in step 1 (id_rsa). and <name> is a name you can choose.

Now, when you clone a github repository use this sintax: 


    git clone git@repo_<name>:repository_usual_url.git

for example :


    git clone git@repo_daniele:latinos/PlotsConfigurations.git

Now you can “tell” Git which SSH credentials to use through SSH config.


## 4. Set your git local user name

Set a local git user name:


    git config  user.name "your_github_name"
    git config  user.email "your_email@example.com"

Do this for every repository you work in. 