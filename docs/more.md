# Shared NTFS partitons fix
When trying to mount a an NFTS partition shared with Windows in R/W mode, it might be not possible because Windows messes the partition flag and the following message is returned ``Could not mount read-write, trying read-only``
Need to fix before trying to mount:
````bash
sudo umount /data
sudo ntfsfix /dev/nvme0n1p5
sudo mount /dev/nvme0n1p5 /data -rw
````
# dvgrab
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
## Stock repo
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
## Iceman repo
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
For clones (non RDV4), create a file `Makefile.platform` containing `PLATFORM=PM3OTHER` before compiling
Compile `make clean && make all`, install `sudo make install`
Flash the bootloader first `./pm3-flash-bootrom` then flash the image `./pm3-flash-fullimage`
If everything is fine, `ls /dev/ttyA*` should give `/dev/ttyACM0`
## Usage notes
### EM410
````bash
lf em 410x reader
-> EM 410x ID 0F0368568B
lf em 410x clone --uid 0F0368568B
````
### MIFARE 1K
````bash
-> Save the UID, example 0F0368568B
hf search
-> Finds at least one default key, example ffffffffffff
hf mf chk * ? or hf mf mifare
-> dump the keys
hf mf nested 1 0 A ffffffffffff d
-> dump the data
hf mf dump
-> Restore the data
hf mf restore 1 u 0F0368568B
-> Restore the UID
hf mf csetuid 0F0368568B
````
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
