# Assignment 10.1 Clone and run script to setup remote.

This is a the first of the `micro` labs.  Now that we have the larger docker instances, we can review how we set up our remote AWS machines.

For this lab you will **create** (not **clone**) a repository and select this repo as the `template`.  You will have to make sure you are using the same account we added to our orgainzation, `DS5111-FALL2023`.  When you go to create a repo, you should see an option to use a template.  Select the name of this repository as the template.

In the repo you will find a makefile and one shell script.

# Required for this lab
* You should have started your larger AWS instance as per the slides and instructions in the DBT lecture.  You'll need the `public ip`
* The `pem` key to access the remote instance
* A github ssh key to your github account
* The github user name, and email

# Steps to follow
* After creating your repository, clone it to your **LOCAL** machine.  If on windows, please use the Ubuntu subsystem so we all go through the same steps.
* After cloning, cd into the repo
* You should be able to now run `make` and see the familiar echoing of the file to console.  There is only one command, `remote`.  But don't run it yet.
* Edit the `setup_remote.sh` file.  Fill out the required variables with the paths and names requested.
* If all is in place, you should now be able to run `make remote`
    - You should see some output to show you two files were scp'd to your remote
    - You should see output showing your creds as they now set up in your remote.  My example from testing this script follows
```bash
>$ make remote
bash setup_remote.sh
EfrainOlivaresUVA                                      100% 3389    35.4KB/s   00:00
config                                                 100%  118     1.3KB/s   00:00
user.name=EfrainOluvaresUVA
user.email=efrainolivaresuva@gmail.com
```
* Next, ssh to your instance and verify that
    - `~/.ssh/config` exists and has the right key name in it
    - `~/.ssh/<your github key name>` exists
    - if you execute `git config --global --list` your creds show up in the console
    - if you execute `ssh -T git@github.com` you get a message back from github that you connected, (but they don't provide a console)
 
# Grading - 5 points total
* Send a link in Canvas to your repository
* add a screenshot **TO YOUR README.md** of an `ls` showing the files in `~/.ssh`, followed by the `git config...` and `ssh -T...` commands showing the expected input.  Look at [github docs image markdown](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#images)

* Verification Steps:
    - `~/.ssh/config` exists and has the right key name in it
    - ![](/imgs/Screenshot_2023-11-20_110725.png)
    - `~/.ssh/<your github key name>` exists
    - ![](/imgs/Screenshot_2023-11-20_110756.png)
    - if you execute `git config --global --list` your creds show up in the console
    - ![](/imgs/Screenshot_2023-11-20_110834.png)
    - if you execute `ssh -T git@github.com` you get a message back from github that you connected, (but they don't provide a console)
    - ![](/imgs/Screenshot_2023-11-20_110917.png)

# Quiz - 10 points
* A quiz will follow wich will focus just on this content.  It's `open book` or `open internet`.

# Extra credit - 5 points
* Create a new makefile/bash-script pair that
    - checks out one of your repositories, that would fully set up your remote for going straight to work on a new machine.
    - completes the setup by remotely installing `make` and the python env package that was missing
    - **OR** anything you find useful... load data you would use in a project, take the next step and trigger a makefile in a cloned repo to setup the python virtual environment, etc etc.

* Verification Steps:
    - A bash script was made to clone a repo and install dependencies. The screenshot below shows the execution of the script. For the full output see `ouputs/automation-outputs.txt`. Below that is a screenshot confirming the script worked remotely.
    - ![](/imgs/Screenshot_2023-11-20_124905.png)
    - ![](/imgs/Screenshot_2023-11-20_124838.png)
    - Note for simplicity the user should run the `setup_remote.sh` script before running `custom_setup.sh`. This can be done with a single command as demonstrated below.
```bash
(base) dscerbo@DESKTOP-UM1PCBF:~/projects/DS5111_Lab_10_1$ ./setup_remote.sh && ssh -i ~/.ssh/ybt7qf_09192023.pem ubuntu@100.25.203.214 'bash -s' < custom_setup.sh git@github.com:dscer/DS5111_FALL2023_SW2_Lab.git
```

