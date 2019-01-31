# Enabling Num Lock on startup
Numlock is not set by default. Here is how to do it for **tty** and **X11** (both needed)

## For tty
Create a this file ``/usr/local/bin/numlock`` and edit it to include
````console
#!/bin/bash
for tty in /dev/tty{1..6}
do
/usr/bin/setleds -D +num < "$tty";
done
````
Set it as excecutable with ``chmod +x /usr/local/bin/numlock``

Create this file ``/etc/systemd/system/numlock.service`` and edit it to include
````console
[Unit]
Description=numlock

[Service]
ExecStart=/usr/local/bin/numlock
StandardInput=tty
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
````
Enable the service by ``systemctl enable numlock.service``

## For X11
Install ``numlockx`` by running ``pacman -S numlockx``

Edit ``.xinitrc`` and add an entry to invoke numlockx in the background just before invoking the window manager (i3 here)
````console
numlockx &
exec i3
````
