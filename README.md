# Group Onboarding
This repository is a guide for getting started when joining the lacourjansengroup.

This page is still work in progress.

## Work in the group
The group is working at different aspects of Computational Spectroscopy. Depending on your project you will have different tasks and parts of this tutorial will be more useful than others. The structure of this document reflects these differences. As a starting point all group members do extensive calculations which require the use of high perfomance computing clusters (HPC). Therefore you should make sure that you are familiar with how to use linux and these clusters. The other aspects that we treat in our group are:

You may also find other useful information on academic work in our group at the [Artificial PhD student](https://github.com/lacourjansenlab/TheArtificialPhDstudent), which you can get access to by joining the GitHub group.

# Kickoff assignment


This document provides you with the fundamental tools used in your project. You will learn how to
- use the terminal (command line)
- connect to the computer clusters (Habrok, Nieuwpoort, etc.)
- run your first simulation
- analyse the simulations using python
- interpret the results


At the end of this tutorial, you should be able to
- find your way in the terminal using the fundamental commands 
- connect to Habrok either directly from terminal (for mac and linux users) or through Putty (for windows users)
- run your first simulation on the interactive node of Habrok 
- understand the Bead-Spring model and the unit system
- call Python functions
- plot your results using matplotlib
- compare your numerical results to known theory


Throughout this document, you will encounter some tasks. Please complete them in 10 days. You are highly encouraged to talk to each other and collaborate. If you are stuck in any of these steps, ask your supervisor for help. 

---


## Part 1: Introduction to command line

The command line, or terminal, is a text-based interface to the system. You can navigate through files, run programs, and even connect to other computers. For many computational projects, especially those involving computer clusters, the command line is an essential tool.

Here are some fundamental commands you will use:

- `pwd` to print the directory you're currently in
- `ls` to list the files and directories in the current directory
- `cd` to change the directory
- `mkdir` to create a new directory
- `rm` to remove files or directories
- `cp` to copy files or directories

> **DANGER**: Never type `rm -rf *` in your home directory. This will delete everything in your system and it's not reversible.



### Remote connection to Habrok

Make sure that you have access to Habrok, if not request an account from [here](https://wiki.hpc.rug.nl/habrok/introduction/policies#getting_access). To connect to computer clusters like Habrok and Nieuwpoort, you'll use SSH (Secure Shell). SSH allows you to securely connect to another computer over the internet. Click [here](https://wiki.hpc.rug.nl/habrok/connecting_to_the_system/connecting) for more information on how to connect to Habrok

For Mac and Linux users, open the terminal and type:

```bash!
ssh s123456@interactive1.hb.hpc.rug.nl
```

Replace `s123456` by your student number.

There are 4 possible ways of connecting to Habrok. If the above node is irresponsive, you can try the following:

```bash
ssh s123456@login1.hb.hpc.rug.nl
ssh s123456@login2.hb.hpc.rug.nl
ssh s123456@interactive2.hb.hpc.rug.nl
```


For Windows users, you'll need to download and install Putty, a free SSH client. Once installed, open Putty, enter the hostname (e.g., `s123456@interactive1.hb.hpc.rug.nl`), and click 'Open' to connect. More information for Windows users [here](https://wiki.hpc.rug.nl/habrok/connecting_to_the_system/windows)


### Task 1: Complete [this tutorial](https://linuxsurvival.com/linux-tutorial-introduction/) on the command line

Optional task-1: Watch [this video](https://www.youtube.com/watch?v=s3ii48qYBxA) 

Optional task-2: If what you want to do is more complicated than the simple shell commands like above, you will need to write bash scripts. Complete [this tutorial](https://www.shellscript.sh/) on bash scripting to learn more.

### Task 2: Connect to Habrok and type the following command
```bash
echo $USER
```
What is the output on the screen?


## Part 2: Running your first simulation


After connecting to Habrok, you'll navigate to a suitable directory to run your simulation. We will run this simple simulation on the interactive node, but please note that the purpose of the interactive node is to test your simulations. Never run an actual simulation on the login/interactive nodes once you start working your own project.

First, navigate to the scratch partition on Habrok by typing the following.

```bash
cd /scratch/$USER
```

---

We are grateful to Andrea Giuntoli and his group for the inspiration to this page.

[The Giuntoli onboarding](https://giuntoligroup.web.rug.nl/)
