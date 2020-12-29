# Useful stuff
## dvgrab
For capturing video and audio from FireWire cameras (IEEE 1394), you need ``dvgrab``
Install it with ``sudo pacman -S dvgrab``. A typical use would be

````bash
dvgrab --autosplit --timestamp --size 0 --rewind FilesName-
````
## python-pip
If you're a Python programmer you would need PyPA recommended tool for installing Python packages
````bash
sudo pacman -S python-pip
````
## thunar
[thunar](https://wiki.archlinux.org/index.php/Thunar) (a lightweight files manager)
````bash
sudo pacman -S thunar thunar-archive-plugin thunar-media-tags-plugin thunar-volman gvfs tumbler
````
## proxmark3
````bash
git clone https://github.com/proxmark/proxmark3.git
cd proxmark3
git pull
sudo cp -rf driver/77-mm-usb-device-blacklist.rules /etc/udev/rules.d/77-mm-usb-device-blacklist.rules
sudo udevadm control --reload-rules
sudo usermod -aG uucp $USER
sudo pacman -S pcsclite
make clean && make all
cd client
./proxmark3 /dev/ttyACM0
````
## That onion
````bash
sudo pacman -S openvpn dialog
sudo pip3 install protonvpn-cli
sudo protonvpn init
protonvpn examples
sudo protonvpn c --cc US -p udp
sudo pacman -S tor
gpg --verbose --auto-key-locate nodefault,wkd --locate-keys torbrowser@torproject.org
yay -S tor-browser
tor-browser -u
````
