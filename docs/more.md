# Miscelaneous
## dvgrab
For capturing video and audio from FireWire cameras (IEEE 1394), you need ``dvgrab``
Install it with ``sudo pacman -S dvgrab``. A typical use would be

````bash
dvgrab --autosplit --timestamp --size 0 --rewind FilesName-
````
# Blocking internet access for one program
````bash
sudo pacman -S firejail
firejail --net=none program_to_block
````
# Installing debian packages on Arch
````bash
yay -S debtap
debtap -q package.deb (will generate package.pkg.tar.zst)
sudo pacman -U package.pkg.tar.zst
````
# proxmark3
Don't install binaries from AUR, you might need to teak the compilation to match your hardware
## Regular repo
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
## Iceman Repo
````bash
sudo pacman -Sy git base-devel readline bzip2 arm-none-eabi-gcc arm-none-eabi-newlib qt5-base bluez --needed
git clone https://github.com/RfidResearchGroup/proxmark3.git
sudo systemctl stop ModemManager
sudo systemctl disable ModemManager
````
Plug the device and type `sudo dmesg | grep -i usb` if okay something alike should show:
````bash
usb 2-1.2: Product: PM3
usb 2-1.2: Manufacturer: proxmark.org
cdc_acm 2-1.2:1.0: ttyACM0: USB ACM device
````
For clones non RDV4 proxmark create a file `Makefile.platform` containing `PLATFORM=PM3OTHER` before compiling
Compile `make clean && make all`, install `sudo make install`
Flash the bootloader first `./pm3-flash-bootrom` then flash the image `./pm3-flash-fullimage`
If everything is fine, `ls /dev/ttyA*` should give `/dev/ttyACM0`
## Usage

# Smells like onion
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
