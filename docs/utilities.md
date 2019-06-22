# Completing Arch installation
## ZSH
Check current shell with ``echo $SHELL``, then install ZSH and its useful plugins
````console
sudo pacman -S zsh zsh-completions zsh-syntax-highlighting zsh-history-substring-search
````
Launch ZSH by typing ``zsh``. Here is how to launch the configuration script if you missed it
````console
zsh /usr/share/zsh/functions/Newuser/zsh-newuser-install -f
````
To setup ZSH as default shell for root user for example
````console
sudo -s
chsh -s /usr/bin/zsh root
````
## Git
````console
sudo pacman -S git
git config --global color.diff auto
git config --global color.status auto
git config --global user.name "name"
git config --global user.email "email"
````
## Yay
````console
cd ~
git clone https://aur.archlinux.org/yay.git
cd yay
sudo pacman -S base-devel (if not installed)
makepkg -si
````
## Compression and sync utilities
````console
sudo pacman -S p7zip p7zip-plugins unrar tar rsync
````
## Codecs
````console
sudo pacman -S a52dec faac faad2 flac jasper lame libdca libdv gst-libav libmad libmpeg2 libtheora libvorbis libxv wavpack x264 xvidcore flashplugin libdvdcss libdvdread libdvdnav dvd+rw-tools dvdauthor dvgrab gstreamer
````
## ACPI
````console
sudo pacman -S acpi
````
## Fonts
````console
sudo pacman -S adobe-source-sans-pro-fonts aspell-en enchant gst-libav gst-plugins-good icedtea-web jre8-openjdk languagetool libmythes mythes-en pkgstats ttf-anonymous-pro ttf-bitstream-vera ttf-dejavu ttf-droid ttf-gentium ttf-liberation ttf-ubuntu-font-family awesome-terminal-fonts ttf-font-awesome otf-font-awesome
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
## Themes
````console
sudo pacman -S breeze-gtk adapta-gtk-theme arc-gtk-theme arc-solid-gtk-theme deepin-gtk-theme
````
and
````console
sudo pacman -S lxappearance-gtk3 qt5ct
````
## Icons
````console
sudo pacman -S adwaita-icon-theme arc-icon-theme mate-icon-theme sugar-artwork tangerine-icon-theme faenza-icon-theme deepin-icon-theme elementary-icon-theme oxygen-icons-svg adwaita-icon-theme breeze-icons
````
## Cursors
````console
sudo pacman -S xcursor-bluecurve xcursor-flatbed xcursor-neutral xcursor-simpleandsoft xcursor-pinux xcursor-vanilla-dmz xcursor-vanilla-dmz-aa
````
## Screen shot & image utilities
````console
sudo pacman -S scrot feh
````
## and of course...
````console
sudo pacman -S openssh cmatrix neofetch
````
