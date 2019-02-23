# CheatSheet
Nice instructions and suggestions

## Nice Instructions

 * every two hours, take a break!  


## Git Tutorial
Useful links to familiarize with Git

 * Simple Guide: https://rogerdudler.github.io/git-guide/index.html

 * Complete Tutorial: https://git-scm.com/docs/gittutorial

 * Easy-to-use syntax for README: https://www.markdownguide.org/basic-syntax/

```
$ code test
```

###Quick start:

After creating a GitHub account you should associate it with an SSH key on your notebook.

Check if you already have a public SSH key:

```
#Check at the default path for SSH keys:
$ ls -al ~/.ssh
```

You should see on of these files:
 * id_dsa.pub
 * id_ecdsa.pub
 * id_ed25519.pub
 * id_rsa.pub

If none of them are there open a terminal (or GitBash on Windows) and type this to create a new ssh key, using the provided email as a label:

```
$ ssh-keygen -t rsa -b 4096 -C <your_email@example.com>
```

When you're prompted to "Enter a file in which to save the key," press Enter to use the default file location (or choose a different location).

Then start SSH-Agent and add your private key:

```
# start the ssh-agent in the background
$ eval $(ssh-agent -s)
> Agent pid 59566

$ ssh-add ~/.ssh/id_rsa
```

Now add the ssh to your GutHub account: 

```
$ cat ~/.ssh/id_rsa
```
	
Copy the content and add it to "SSH and GPG keys" in your GitHub account.

Now you can start using git command (tutorial above).
=======
```
$ code test
```
>>>>>>> 88205d16e657b25bbb8a92ed5b52cd1d5de951f7
