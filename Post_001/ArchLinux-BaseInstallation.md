After years on Windows and having this old Asus EeePC 11010HA taking dust on the storage I decided to give it a second life following the discovery of [Arch Linux](https://www.archlinux.org) and [Xmonad](http://xmonad.org/) from a friend whose working on a startup.  
I tried a lot of other windows and Linux distribution in the past on this machine without success mainly related to the video driver which is the Intel GMA500.  
This post summarize how to setup Arch linux on a laptop.

Preparing the USB drive
===
The first setup before installing Arch linux is to create a USB boot drive Installation. As I don't have any linux machine for years I needed to find a way to create this USB boot drive on windows.

Download require
---
- [Yumi Multiboot](http://www.pendrivelinux.com/yumi-multiboot-usb-creator/) : This will allow you to create the USB Boot drive simply. If you have chocolatey install on your machine you can run the following command ```powershell
choco install yumi```
- [Arch Linux ISO](https://www.archlinux.org/download/): This is the ISO image

Creating the USB Boot drive
---
1. Open Yumi and set the parameters as below. Don't forget to check "*we Will Fat32 Format F: Drive!* "  
   ![Yumi setting](.\Yumi Setting.PNG)  

2. Click "*Create*" and wait  
   ![Yumi Running](.\Yumi Running.PNG)

Installation of Arch Linux
===
The instruction you will see below come from mainly from the [video](https://www.youtube.com/watch?v=Wqh9AQt3nho) that *Goguda55 Tech Tutorial* made. Thank you to him.
I added some information about during the initial installation process how to setup install all the package required to be able to set the Wifi.

Instruction
--
1. **Select from the Arch linux install that you want**  
   You can select the installation you want to do. In our case we want to install the i686 which is the 32 bits version of Arch Linux.  

   ![Arch Install](.\01 - ArchLinux Boot Screen.PNG)  

   This will bring you to the basic command prompt  

   ![Arch base prompt](.\02 - ArchLinux Startup prompt.PNG)  

2. **Find the install drive name**  
   Run the command  
   ```
   fdisk -l
   ```  
   This will list all the disk you have on your machine. In my case the command return
   In my case the drive on which I want to install Arch Linux is */dev/sda*

3. **Create the partition on your hard drive**  
   We want to create two partition on the drive /dev/sda
    * Swap partition : half of the size of your memory
    * Data partition : We will create a single partition for all the rest. We won't try to be clever and create different partition for different folder.  

   Run the command below to start the partition manager :  
   ``` batsh
   cfdisk /dev/sda
   ```  

4. **Format the main partition and mount the disk**   
  ```batsh  
  mkfs.ext4 /dev/sda2  
  mount /dev/sda2 /mnt
  ```



1. fdisk -l
2. cfdisk /dev/sda
3. mkfs.ext4 /dev/sda2
4. mount /dev/sda2 /mnt
5. mkswap /dev/sda1
6. swapon /dev/sda1
7. wifi-menu
8. pacstrap /mnt base base-devel
9. arch-chroot /mnt
10. passwd
11. nano /etc/locale.gen
12. locale-gen
13. cd /usr/share/zoneinfo
14. ln -s /usr/share/zoneinfo/Hongkong /etc/localtime
15. echo archZucky > /etc/hostname
16. useradd -m -g users -G wheel,storage,power -s /bin/bash {username}
17. passwd {userName}
18. pacman -S sudo
19. pacman -S bash-completion
19. pacman -S iproute2
19. pacman -S wpa_supplicant
19. pacman -S wpa_supplicant_gui
19. pacman -S dialog
20. pacman -S wireless_tools
20. pacman -S netctl
20. pacman -S systemd-networkd



20. ip link
21. systemctl enable dhcpcd@NAME-OF-THE-NETWORK.service

16. pacman -S grub-bios
17. grub-install /dev/sda
18. mkinitcpio -p linux
19. grub-mkconfig -o /boot/grub/grub.cfg
20. exit
21. genfstab /mnt >> /mnt/etc/fstab
22. umount /mnt
