If you follow the previous article of this serie about setting Arch Linux, you should be at the point where you have a base Linux system.

In this post I will focus on the creation of users, installation of useful utility and setup of some of the base services. 

Creation of users
-----------------
Following the reboot of your ArchLinux installation you will be asked to connect. Use root (I promess this is hte last time we will use it) and the password you setup in the previous article

We are creating a new account and add it in the group wheel by default. The group wheel is a group that allow you to run some restricted command from that user. 

    useradd -m -g wheel [account name]
    passd [account name]

The next step is to grant to the wheel group the right to run sudo. 'sudo' stand for 'Superuser Do' and will allow us to continue the installation on a more secure maner.
Install sudo
    pacman -S sudo

We have to edit the sudo configuration file to grant the permission. Editing the sudo configuraiton need to to be done using visudo. This ensure when we are saving the file that it is valid and wont lock us.
    visudo

We are at that point in our favorite text editor, VI :-). I hope you remember your basic here. The only key will need are 
    - i : insert
    - esc : exit the edit mode
    - :wq : save and quit

At the end of the file you will see a section that contain a lot of commented line (starting with #) which represent some template.
We want to add there the following lines
    ## Allow members of group wheel to execute any command. 
    %wheel ALL=(ALL) ALL

follow this link if you want to read more about sudo [https://wiki.archlinux.org/index.php/Sudo]

Installation of utility
-----------------------

1. yaourt
    :
