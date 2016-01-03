1. netctl to use with wifi-menu

2. Check the current service used for network. Only one network service can be started
   systemctl --type=service

3. You can use 'wifi-menu -o' to set your current connection

4. find your profile name ls /etc/netctl

5. start and enable your profile
netctl start profile
netctl enable profile


restart



sudo bash-completion
19. pacman -S

16. useradd -m -g users -G wheel,storage,power -s /bin/bash {username}
17. passwd {userName}
19. pacman -S iproute2
19. pacman -S wpa_supplicant
19. pacman -S wpa_supplicant_gui
19. pacman -S dialog
20. pacman -S wireless_tools
20. pacman -S netctl
20. pacman -S systemd-networkd

20. ip link
21. systemctl enable dhcpcd@NAME-OF-THE-NETWORK.service
