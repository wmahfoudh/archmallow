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
## i3lock and multiple keyboards
``i3lock`` is the simplest way to implement a lock screen. Normally, this is how I would invoke it ``/usr/bin/i3lock -c 000000 -u`` (``-c 000000`` for a black locak screen and ``-u`` to disable the unlock indicator).

Again, that's fine, but it won't work with multiple keyboards. If the screen gets locked when the keyboard language is other than the unlocking password language, the unlocker won't work. A simple workaround to this problem is setting the keyboard to English just before the screen gets locked (for example, if your password was wet using the English keyborad). For this we will create a shell script to wrap those commands and call the wrapper instead of directly invoking ``i3lock``.
So create a file called ``.i3lock-wrapper`` in your home directory, paste the following in it and make it executable
````bash
#!/bin/bash
2
3 setxkbmap us
4 /usr/bin/i3lock -c 000000 -u
````
Now inside i3 .config file, you can bind the screen lock with (mod+o for example)
````console
bindcode $mod+32 exec ~/.i3lock-wrapper
````
## Locking the computer for inactivity
To do so, ``xautolock`` must be called to run in the background before calling the i3 window manager. This is done in the ``.xinitrc`` file
````bash
xautolock -time 1 -corners ---- -locker '~/.i3lock-wrapper' &
exec i3
````
- ``-time 1`` means that the screen will be locked after 1 minte of inactivity
- ``-corners ----`` mean that the screen won't lock if the mouse pointer is located at any corner. This is particularly useful if you're watching a movie or anything similar and don't want the screen to lock
- ``-locker '~/.i3lock-wrapper'`` means the the locker to be used is our wrapper defined previously
## Screen capture
This can be achieved using ``scrot`` with the following bindings (captured images are saved in ``~/screenshot``)
````console
# Full screen capture (PrintScreen)
bindcode 107 exec --no-startup-id scrot ~/screenshots/`date +%Y-%m-%d-%H-%M-%S`.png
# Window capture (mod+PrintScreen)
bindcode $mod+107 exec --no-startup-id scrot -u ~/screenshots/`date +%Y-%m-%d-%H-%M-%S`.png
# Region screenshoot (mod+Shift+PAUSE) (will show selector arrows to draw a rectangle area)
bindcode $mod+127 exec --no-startup-id scrot -s ~/screenshots/`date +%Y-%m-%d-%H-%M-%S`.png
````
## Change the keyboard layout
and display it in the status bar: it's all explained [here](https://github.com/porras/i3-keyboard-layout). Create ``~/.i3-keyboard-layout`` with [this](https://github.com/porras/i3-keyboard-layout/blob/master/i3-keyboard-layout) contents. In the ``bar`` section of i3 config file replace this
````console
status_command i3status
````
by this
````console
status_command i3status | ~/.i3-keyboard-layout i3status
````
The only thing remainingis to bind keyboards to some keys. Personally, I prefer on key to cycle the 3 languages I use. I have these lines in my i3 config file
````console
# cycle keyboards (c)
bindcode $mod+54 exec --no-startup-id ~/.i3-keyboard-layout cycle us fr ar
````
