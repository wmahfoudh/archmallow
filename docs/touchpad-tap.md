# Enabling touchpad tapping
1. Install ``libinput``
2. Edit your touchpad configuration file ``/etc/X11/xorg.conf.d/30-touchpad.conf`` and ensure it has an ``InputClass`` section similar the this
````console
Section "InputClass"
Identifier "touchpad"
Driver "libinput"
MatchIsTouchpad "on"
Option "tapping" "on"
Option "AccelProfile" "adaptive"
Option "TappingButtonMap" "lrm"
EndSection
````
You would have:
- one finger tap a left mouse button click,
- two finger a right mouse click and
- three finger a scroll wheel click
