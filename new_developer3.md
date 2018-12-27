Version 0.0.6
The intent of this document is to get developers up to speed on sther.co as quickly as possible.

This is not ment to be exhaustive and in some cases will site other documentation but it is my hope that this will make the process of getting set up in under and hours.

This document assume you are using Debian Linux Stretch using virtualbox as my virtualization engine. That said this should work on other Uni\* machine and even windows with a little modifcation

also in cases where a file or directory is named .hiddenfilename/.hiddendirectory I am calling it
dothiddenfilename so I can include it in the documentation/example directory and it is not a pain to find.

I have also organized file by directory inside examples/

I would be very doable to create a install script that did all or most of this but this may be done later.

# 1.  Download vagrant from: https://www.vagrantup.com/downloads.html

# 2.  install vagrant
```sudo dpkg -i vagrant_2.2.2_x86_64.deb```

# 3.  Download and install virtualbox from https://www.virtualbox.org/wiki/Linux_Downloads
### A. Add the virtualbox repository to /etc/apt/sources.list (changing strecht to whatever distribution you are using.)


```    sudo echo 'deb https://download.virtualbox.org/virtualbox/debian <stretch> contrib' >/etc/apt/sources.list```
```    sudo wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -```
```    sudo wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O- | sudo apt-key add -```
```    sudo apt-get update```
```    sudo apt-get install virtualbox-6.0```


# 4.  install Homestead based on <https://laravel.com/docs/5.7/homestead>

```cd ~/```
```vagrant box add laravel/homestead```
```git clone https://github.com/laravel/homestead.git ~/Homestead```
```cd ~homestead```
### A. Find the latest tag with
```
git tag
```
### B. Install the latest tag ie v7.20.0
```    
git checkout v7.20.0
bash init.sh
```
### C. You need to edit Homestead.yaml. My Homestead/Homestead.yaml is included in examples/Homestead/Homestead.yaml
```
nano Homestead.yaml
```
### D. The .ssh directory must be created
```
$ mkdir ~/.ssh
```
### E. Update your /etc/hosts file to include pointers to the test websites based on my example in examples/etc/hosts.
### F. add examples/dotbashrc to ~/.bashrc so vagrant can be called with the command sther
```
cat  examples/dotbashrc >> ~/.bashrc`
```
### G. Reprocess the .bashrc file (this only need to be done now. Since next time you log in it will happen automatically)
```
source ~/.bashrc`
```

# 5.  Setting ssh (based on <https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/>)
### A . Create a ssh key
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com" -f ~/.ssh/your_email@example.com_rsa
```
### B. Adding key to based on (github <https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/>)
####    1\. Install xclip
```
sudo apt-get install xclip
```
####    2\. xclip keyfile
```
xclip -sel clip < ~/.ssh/your_email@example.com_rsa.pub
```
###      C. Upload the key to github
####        i\. In the upper-right corner of any page, click your profile photo, then click Settings.
####        ii\. Authentication keysIn the user settings sidebar, click SSH and GPG keys.
####        iii\. SSH Key button
####        iv\. Click New SSH key or Add SSH key.
####        v\. In the "Title" field, add a descriptive label for the new key. For example, if you're using a personal Mac, you might call this key "Personal MacBook Air".The key fieldPaste your key into the "Key" field.
####        vi\. The Add key button
####        vii\. Click Add SSH key.
####       viii\. If prompted, confirm your GitHub password.

###        D. set up .ssh/config based on examples/dotssh/config
###        E. Test ssh/GitHub (based on https://help.github.com/articles/testing-your-ssh-connection/)
##         Please keep in mind the username has to be git no matter what your username is.**
```
    ssh -T git@github.com
```

# 6.  Set up git
##      A. set up the directory structure we will be using
```
mkdir ~/code
mkdir ~/code/sther
mkdir ~/code/sther/current
mkdir ~/code/sther/master
mkdir ~/code/sther/your_branch_name
```
##      B. git clone the files from github remember to use git@github.com also that the branch **_develop_** is the current production code
```     
git clone ssh://git@github.com/dmrobotix/sther.git ~/code/sther/master
git clone -b develop ssh://git@github.com/dmrobotix/sther.git ~/code/sther/current
```
##      C. install the .env which you will need to get via discord or similar
```
cp path_to_dotenv ~/code/sther/current\```
```

# 7.  Getting Homestead ready and testing it
##        A. Now is a good time to start vagrant (this may take a while)
```
sther up
```
##        B. ssh into the vagrant/homestead virtualbox
```
sther ssh
```
##        C. switch to the current tree via   
```
cd code/sther/current/`
```
##        D. install laravel via composer
```
composer install
```
##      E. Exit the terminal window
```    
exit
```
##      F. put the following url into your browser https://sther.current.test
##      G. if everything works you are set. If you do not have an icon in the upper left of your screen. To fix this right click on open image in new tab. It will give you an error message. Click threw to load the page anyway.


# 8.  Creating a new branch
##      A. Input the develop branch as the first step of creating your own branch
```
git clone -b develop ssh://git@github.com/dmrobotix/sther.git ~/code/sther/your_branch_name
```
##      B. change to the correct directory
```
cd ~/code/sther/your_branch_name`
```
##      C. create the branch
```    
git checkout -b your_branch_name
git checkout -your_branch_name
git push origin test
git push -u origin HEAD
```
##      D. ssh into the vagrant/homestead virtualbox
```
sther ssh
```
##      E. switch to the current tree via
```
cd code/sther/your_branch_name/
```
##      F. install laravel via  composer
```
composer install
```
##      G. exit the terminal
```    
exit
```
##      G. copy .env to your branch

```cp ~/code/sther/current/.env ~/code/sther/your_branch_name```

        once you download and install Atom, you can create a project. The best thing to do is download the github repo, create your own branch, and then import that directory as a new project into atom.

    then you'll see all the code files there.
    I also need to add you to the repo. do you have a github acount?


     https://getuikit.com/docs/
