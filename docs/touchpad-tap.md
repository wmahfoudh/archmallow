# Enabling touchpad tapping
Install ``libinput`` and edit the touchpad configuration file ``/etc/X11/xorg.conf.d/30-touchpad.conf``. Ensure it has the following ``InputClass`` section
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
Adding this section would activate:
- one finger tap a left mouse button click
- two finger a right mouse click
- three finger a scroll wheel click
