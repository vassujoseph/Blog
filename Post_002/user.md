If you followed the previous article of the series about setting up Arch Linux, you should be at the point where you now have a base Linux system.

In this post I will focus on the creation of a users, installing and setting up *sudo* and disabling the root account. You can find detailed information by following this [link](https://wiki.archlinux.org/index.php/Sudo).

# Creating a user

Following the reboot of your ArchLinux installation you will be asked to connect. Use root and the password you setup in the previous article.

We are going to create a new account and add it to the group wheel by default. The group _wheel_ is a group that allows you to run some restricted commands from that user. As I want this account to be an advanced power user, this is the group I want to be part of.
````batch
useradd -m -g wheel [account name]
passd [account name]
```  

## Setting Sudo

The next step is to install and set up *sudo* to allow the group wheel to run command in elevate mode. 'sudo' stands for 'Superuser Do' and will allow us to continue the installation without using the root account.

    1. ### Installing sudo

    ```batch
    pacman -S sudo
    ```  
    2. ## Setting sudo

    We have to edit the sudo configuration file to grant the permission. Editing the sudo configuraiton needs to to be done using visudo. This ensures when we are saving the file that it is valid and wont lock us.  
    ```batch
    visudo
    ```  

    We are at that point in our favorite text editor, VI :-). I hope you remember your basics here. The only keys you will need are
        - i : insert
        - esc : exit the edit mode
        - :wq : save and quit

    At the end of the file you will see a section that contains a lot of commented lines (starting with #) which represent some templates. We want to add there the following lines.  
    ##Allow members of group wheel to execute any command.
    %wheel ALL=(ALL) ALL

Follow this link if you want to read more about [sudo](https://wiki.archlinux.org/index.php/Sudo).

## Disable root

Disabling the *root* account is not mandatory, but is strongly recommended as everyone knows the root account on Linux.  

1. ### Disconnect from the current root session
  ```batch
  exit
    ```   
2. ### Connect with your user account
3. ### Disable root
The best way to disable the root account is to lock it. For that run the following command.  
```batch
sudo passwd -l root
```  

# Summary

This was a simple article that allows you to secure your base installation in the most basic way. In the next article we will look at how to set up some of the basic services and start to install some basic applications.
