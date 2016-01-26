For this article we will focus on network setup (at least what I've found so far) and will look at some of the useful commands that I now use often.

Setting up the network, and more specifically the wifi can be traumatic. However, even without X windows there are some nice simple tools to help you to setup the wifi connection (like 'wifi-menu' that we used earlier).

If you follow the step to set up the base installation from this [article](Need to define), you should already have from your base installation the packages [netctl](https://wiki.archlinux.org/index.php/netctl) and [dialog](http://linuxcommand.org/lc3_adv_dialog.php). *netctl* is a batch script built on top of systemctl that allows you to start or stop the network profile configuration service.

# Connecting Manually

Before trying to connect using some auto detection, it would be good to understand what is happening under the hood. *netctl* is a simple command that allow you to list available profiles, start a profile or stop a profile. In this section we will first look at how to setup a wired connection followed by a wifi one, and then get a quick overview of the netctl command line tool.


## Setting up an Ethernet profile

*netctl* stores the connection profile in the folder */etc/netctl*. This folder has a child one named */etc/netctl/example* which contain a set of different example profiles. We are interested here in the example profile whose name starts with 'ethernet'. In my case I have 3 examples:  

  - ethernet-custom : allows you to see all the available fields you can set up
  - ethernet-dhcp : example to connect and get the IP address from a DHCP server
  - ethernet-static : example to setup a profile using a static IP address  

As my router is doing as well DHCP server for me, I will simply set up the profile using ethernet-dhcp as a sample. The steps we have to do are:  

1. ### Find the ethernet network interface name
Linux has a command line *ip* utility that allow you to query and update the network interfaces. The command line to run to list the network interfaces is  

  ```batch
  ip link
  ```  

  The result of the query is in my case
  ![IpLinkResult](./IpLinkResult.png)  
  The ethernet adaptor name starts everytime with *enp* - in my case the name is *enp3s0*  

1. ### Copy the example */etc/netctl/example/ethernet-dhcp* to */etc/netctl*  
We need to copy the example file */etc/netctl/example/ethernet-dhcp* to the folder */etc/netctl* and give it a name that is meaningful. In my case I will name it *enp3s0-ethernet-dhcp* because it's a good representation of the profile's meaning.
Back to the command shell to copy the file using :

  ```batch
  cp /etc/netctl/example/ethernet-dhcp /etc/netctl/enp3s0-ethernet-dhcp
  ```  

3. ### Edit the Profile
You can use any text editor that you want - *vim* is the one I'm using every time. We want to open */etc/netctl/enp3s0-ethernet-dhcp* to change the property *Interface* with the one we found at step 1.
The content you should have in the file at minimum is :

  ![profile Content](.\enp3s0-ethernet-dhcp-Content.png)

4. ### Check the permission
The profile we just updated is good, however this is not protected against being seen by unauthorised users. This profile doesn't have a lot of important information, although it will do later on for the wifi setup. We will change the password using the command line *chmod* and set read/write only for the root users.  

  ```batch
  chmod 600 enp3s0-ethernet-dhcp
  ```

5. ### Plug in the ethernet cable and start the profile
We can now plug in our ethernet cable and start the profile. We will use the command line netctl. The command to start the profile is   

  ```batch
  sudo netctl enp3s0-ethernet-dhcp
  ```

  The best command to test that the profile is enabled and that you can access the network is to ping the google dhcp server with the address 8.8.8.8 :-)

## Setting wifi profile

If you installed the package *dialog* in the first post about installing *archlinix*, this allows you to use a simple user interface that doesn't require X windows to be installed. The command we will use is *wifi-menu*, which is a simple script built on top of netctl.

```
Please always use the command *wifi-menu* with the option *-o* to be sure that the password is hashed in the profile file.
```
Running the command *wifi-menu* will create the profile file in the folder */etc/netctl* and connect you to the network at the same time. You can even run the command again to connect to the wifi anytime you want to change the connection. The command you have to run is the following

```batch
sudo wifi-menu -o
```  

You will see the following displayed:

![wifi-menu](.\wifi-menu.png)

Creating a wifi profile is simple with the use of *wifi-menu*. However you can also create a wifi profile using the same type of manual steps as we used to set up the ethernet connection. The hardest part I found about doing that is that you need to know the wifi security type and you may have to put your password in clear.
