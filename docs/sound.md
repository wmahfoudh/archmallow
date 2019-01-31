# Notes on sound setup
## Installation
Install ``alsa-utils`` and ``alsa-plugins`` to have the needed configuration utilities and high quality sampling capability
````console
sudo pacman -S alsa-utils alsa-plugins
````
To control the volume run ``alsamixer``. 'MM' means that the channel is muted, '00' means open, press 'm' to unmut it

For testing the speakers you can run ``speaker-test -c 2`` and for saving the current ``alsamixer`` settings run ``sudo alsactl store``

Below are various examples to play with
````console
amixer scontrols
amixer set Master unmute
amixer set Master mute
amixer set Master toggle
amixer set 'Speaker' toggle & amixer set 'Master' toggle
````
## Binding volume change
This example shows how to bind some function keys to changing volume and toggling mute in i3 config file
````console
#audio controls mod+(F10 F9 F11 F7 F8 F6)
bindcode $mod+76 exec amixer set 'Speaker' 1%+
bindcode $mod+75 exec amixer set 'Speaker' 1%-
bindcode $mod+95 exec amixer set 'Speaker' toggle & amixer set 'Master' toggle
````
