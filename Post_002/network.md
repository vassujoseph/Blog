1. netctl to use with wifi-menu

2. Check the current service used for network. Only one network service can be started
   systemctl --type=service 

3. You can use 'wifi-menu -o' to set your current connection

4. find your profile name ls /etc/netctl

5. start and enable your profile
netctl start profile
netctl enable profile


restart



