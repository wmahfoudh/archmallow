## Sound related
````console
sudo pacman -S alsa-utils
alsamixer (MM=muted, 00=open, press m to unmute)
sudo alsactl store
speaker-test -c 2
amixer scontrols
amixer set Master unmute
amixer set Master mute
amixer set Master toggle
amixer set 'Speaker' toggle & amixer set 'Master' toggle
````
