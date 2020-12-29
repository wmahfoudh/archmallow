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
sudo pacman -Syu xorg plasma-desktop plasma-wayland-session plasma-wayland-protocols kde-applications sddm sddm-kcm
sudo pacman -S bluedevil plasma-nm sshfs
sudo pacman -S firefox terminator codeblocks sshfs
sudo systemctl enable sddm.service
````
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
sudo pacman -S openssh cmatrix neofetch acpi p7zip unrar tar rsync
````
