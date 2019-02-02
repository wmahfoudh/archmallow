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
I use ``bindcode`` instead of ``bindsym`` to bind keys to their actions. The reason is that I have multiple keyboard layouts (English, French and Arabic) and using bindsym, you have to reproduce shortcuts in the active keyboard mapping, which is not practical and sometimes not possible (case of the Arabic keyboard). To display all keycodes and their respective keys type ``xmodmap -pke``. If you want to get the keycodes interctively just use ``xev``
## Locking the screen
``i3lock`` is the simplest way to implement a lock screen. Normally, this is how I would invoke it ``/usr/bin/i3lock -c 000000 -u`` (``-c 000000`` for a black locak screen and ``-u`` to disable the unlock indicator).

Again, that's fine, but it won't work with multiple keyboards. If the screen gets locked when the keyboard language is other than the unlocking password language, the unlocker won't work. A simple workaround to this problem is setting the keyboard to English just before the screen gets locked (for example, if your password was wet using the English keyborad). For this we will create a shell script to wrap those commands and call the wrapper instead of directly invoking ``i3lock``.
So create a file called ``.i3lock-wrapper`` in your home directory, paste the following in it and make it executable
````bash
#!/bin/bash
2
3 setxkbmap us
4 /usr/bin/i3lock -c 000000 -u
````
Now inside i3 .config file, you can bind the screen lock as follows
````console
bindcode $mod+32 exec ~/.i3lock-wrapper
````
