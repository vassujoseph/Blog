If you follow the previous article of the  serie about setting Arch Linux, you should be at the point where you have a base Linux system.

In this post I will focus on the creation of a users, installing and setting *sudo* and disabling the root account. You can find detailed information by following this [link](
https://wiki.archlinux.org/index.php/Sudo)

Creation of users
-----------------
Following the reboot of your ArchLinux installation you will be asked to connect. Use root and the password you setup in the previous article

We are creating a new account and add it in the group wheel by default. The group wheel is a group that allow you to run some restricted command from that user. As I want this account to be advance power, this is the group I want to be part of.
````batch
useradd -m -g wheel [account name]
passd [account name]
```  

Setting Sudo
-----------
The next step is to install and set *sudo* to allow the group wheel to run command on elevate mode. 'sudo' stand for 'Superuser Do' and will allow us to continue the installation without using the root account.

1. **Installing sudo**  
```batch
pacman -S sudo
```  
2. **Setting sudo**  
We have to edit the sudo configuration file to grant the permission. Editing the sudo configuraiton need to to be done using visudo. This ensure when we are saving the file that it is valid and wont lock us.  
```batch
visudo
```  

We are at that point in our favorite text editor, VI :-). I hope you remember your basic here. The only key will need are
    - i : insert
    - esc : exit the edit mode
    - :wq : save and quit

At the end of the file you will see a section that contain a lot of commented line (starting with #) which represent some template. We want to add there the following lines.  
    ## Allow members of group wheel to execute any command.
    %wheel ALL=(ALL) ALL

follow this link if you want to read more about [sudo](https://wiki.archlinux.org/index.php/Sudo)

Disable root
-----------
Disabling the *root* account is not mandatory, but is strongly recommended as everyone know the root account on Linux.  

1. **Disconnect from the current root session**  
  ```batch
  exit
    ```   
2. **Connect with your user account**  
3. **Disable root**  
The best way to disable the rpot account is to lock it. For that run the following command.  
```batch
sudo passwd -l root
```  

Summary
------
This was a simple quick article that allow you to secure your base installation with the basic. In the next article we will look at how to set some of the basic service and start to install some basic
