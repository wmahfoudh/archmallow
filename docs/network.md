# Network Manager
## Installation
````console
sudo pacman -S networkmanager network-manager-applet
````
To check if ``dhcpcd`` or ``netctl`` are enbled, enter
````console
systemctl --type=service
````
In case yes, stop and then diable them before enabling Network Manager
````console
sudo systemctl enable NetworkManager.service
````
## Ethernet related commands
````console
nmcli con show
nmcli dev status
nmcli con add type ethernet con-name LAN_CONNECTION_NAME ifname DEVICE
````
## Wifi related commands
````console
nmcli d wifi list
nmcli d wifi connect WIFI_SSID password PASSWORD
````
## Hidden networks
````console
nmcli con add con-name CONNECTION_NAME ifname wlan0 type wifi ssid WIFI
nmcli con modify CONNECTION_NAME wifi-sec.key-mgmt wpa-psk
nmcli con modify CONNECTION_NAME wifi-sec.psk PASSWORD
nmcli con up CONNECTION_NAME
````
## Other commands
````console
nmcli radio wifi on
nmcli radio wifi off
nmcli con mod CONNECTION_NAME ipv4.dns "8.8.8.8 8.8.4.4"
````