# Completing Arch installation
## Git
````console
sudo pacman -S git
git config --global color.diff auto
git config --global color.status auto
git config --global user.name "name"
git config --global user.email "email-address"
ssh-keygen -t ed25519 -C "email-address"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/newly-generated-private-key
ssh -T git@github.com
git remote -v
git remote set-url origin  git@github.com:user/repo.git
````
## ZSH
Check current shell with ``echo $SHELL``, then install ZSH and its useful plugins
````console
sudo pacman -S zsh zsh-completions zsh-syntax-highlighting zsh-history-substring-search
````
Launch ZSH by typing ``zsh``. Here is how to launch the configuration script if you missed it
````console
zsh /usr/share/zsh/functions/Newuser/zsh-newuser-install -f
````
Clone Autosuggestions
````console
git clone https://github.com/zsh-users/zsh-autosuggestions ~/.zsh/zsh-autosuggestions
````
Add it to `.zshrc`
````console
source ~/.zsh/zsh-autosuggestions/zsh-autosuggestions.zsh
````
To setup ZSH as default shell for root user for example
````console
sudo -s
chsh -s /usr/bin/zsh root
````
## Yay
````console
cd ~
git clone https://aur.archlinux.org/yay.git
cd yay
sudo pacman -S base-devel (if not installed)
makepkg -si
````
## Sound
````console
sudo pacman -S alsa-tools alsa-utils asoundconf sof-firmware alsa-ucm-conf
sudo pacman -S pulseaudio pulseaudio-alsa pulseaudio-bluetooth pulseaudio-equalizer pamixer pulsemixer
````
## KDE
````console
sudo pacman -S xorg plasma-desktop plasma-wayland-session plasma-wayland-protocols kde-applications sddm sddm-kcm
(or instead of kde-applications the ones I prefer)
sudo pacman -S ark cantor dolphin dolphin-plugins ffmpegthumbs gwenview kamera kamoso kate kcachegrind kcalc kcharselect kcolorchooser kcron kdeconnect kdegraphics-mobipocket kdegraphics-thumbnailers kdenetwork-filesharing kdenlive kdesdk-thumbnailers kdf kfind kget khelpcenter kmix kmousetool kmouth kmplot konsole konversation ktorrent ktouch kwalletmanager kwave kwrite okular partitionmanager signon-kwallet-extension spectacle svgpart sweeper umbrello zeroconf-ioslave
sudo pacman -S bluedevil plasma-nm sshfs
sudo pacman -S firefox terminator codeblocks sshfs
sudo systemctl enable sddm.service
````
In some cases the profile pictures do not show at statup in SDDM, try resizing the image to 256x256 or rename it to .face.icon and copy it to home folder and then run
````console
setfacl -m u:sddm:x /home/user
setfacl -m u:sddm:r /home/user/.face.icon
````
Deactivate the Tool Tips interfering with contact menus in Settings <Worskapce behaviour><General behaviour>
  
## Printer
````console
sudo pacman -S cups cups-pdf ghostscript libcups
sudo usermod -aG lp $USER
sudo groupadd lpadmin
sudo usermod -aG lpadmin $USER
sudo systemctl enable cups.service
sudo systemctl start cups.service (cups web server available at http://localhost:631/)
nano /etc/cups/cups-pdf.conf (to modify pdf printing default settings, it is also better to restart whenver adding a new driver)
yay -S epson-inkjet-printer-escpr
````
## Scanner
````console
sudo pacman -S imagescan
yay -S imagescan-plugin-networkscan
sudo nano /etc/utsushi/utsushi.conf
````
add the following in the [devices] section and then reboot
````console
dev2.udi    = esci:networkscan://192.168.0.137:1865
dev2.model  = L3150
dev2.vendor = EPSON
````
Access the scanner utility with `utsushi`
## Codecs
````console
sudo pacman -S a52dec faac faad2 flac jasper lame libdca libdv gst-libav libmad libmpeg2 libtheora libvorbis libxv wavpack x264 xvidcore flashplugin libdvdcss libdvdread libdvdnav dvd+rw-tools dvdauthor dvgrab gstreamer
````
## Virtualbox
````console
sudo pacman -S virtualbox virtualbox-guest-iso (chose virtualbox-host-modules-arch for linux kernel)
yay -S  virtualbox-ext-oracle
sudo groupadd vboxusers (sometimes needs to be added manually)
sudo usermod -aG vboxusers user
````
## Makeup
### Fonts
````console
sudo pacman -S adobe-source-sans-pro-fonts aspell-en enchant gst-libav gst-plugins-good icedtea-web jre8-openjdk languagetool libmythes mythes-en pkgstats ttf-anonymous-pro ttf-bitstream-vera ttf-dejavu ttf-droid ttf-liberation ttf-ubuntu-font-family awesome-terminal-fonts ttf-font-awesome otf-font-awesome
yay -S ttf-win10
````
List available fonts with
````console
fc-list -b | grep 'family:'
fc-list -b | grep 'fullname:'
fc-list : file
````
To change tty font create or edit ``/etc/vconsole.conf`` as follows
````console
FONT=LatGrkCyr-8x16.psfu
FONT_MAP=8859-2
````
### Themes
````console
sudo pacman -S breeze-gtk adapta-gtk-theme arc-gtk-theme arc-solid-gtk-theme deepin-gtk-theme
````
and
````console
sudo pacman -S lxappearance-gtk3 qt5ct
````
### Icons
````console
sudo pacman -S adwaita-icon-theme arc-icon-theme mate-icon-theme sugar-artwork tangerine-icon-theme faenza-icon-theme deepin-icon-theme elementary-icon-theme oxygen-icons-svg adwaita-icon-theme breeze-icons
````
### Cursors
````console
sudo pacman -S xcursor-bluecurve xcursor-flatbed xcursor-neutral xcursor-simpleandsoft xcursor-pinux xcursor-vanilla-dmz xcursor-vanilla-dmz-aa
````
## Miscellaneous
````console
sudo pacman -S openssh cmatrix neofetch acpi p7zip tar rsync dvgrab python-pip openvpn dialog usbutils qbittorrent python-pip dvgrab
yay -S rar
sudo pacman -S mediainfo mediainfo-gui
sudo pacman -S ardour audacity vlc obs-studio blender synfigstudio kdenlive krita
sudo pacman -S mypaint mypaint-brushes mypaint-brushes1 libmypaint
sudo pacman -S gimp rawtherapee darktable
sudo pacman -S picard
yay -S picard-plugins-git
````
