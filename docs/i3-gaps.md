# Installing i3-gaps
Installing the X display server 
````console
sudo pacman -S xorg-server xorg-xinit xorg-xlsfonts xautolock xorg-xprop
````
I prefer i3-gaps over regular i3 for the nice gap effect between windows, but it's not a regular Arch package, it's available on the AUR. Install it with yay (or equivalent)
````console
yay -S i3-gaps
sudo pacman -S i3blocks i3lock i3status
sudo pacman -S compton compton-conf
````
``i3blocks`` is a scheduler for the status line scripts, ``i3lock`` will allow us to lock the screen, ``i3status`` to have a nifty status bar and ``compton`` will allow some windows transparency
# Ricing i3-gaps
## bindcode vs bindsym
I use bindcode and not bindsym to bind keys to their actions. The reason is that I have multiple keyboard layouts (English, French and Arabic) and using bindsym, you have to reproduce shortcuts in the active keyboard mapping, which is not practical and sometimes not possible (case of the Arabic keyboard). To display all keycodes and their respective keys type ``xmodmap -pke``. If you want to get the keycodes interctively just use ``xev``
