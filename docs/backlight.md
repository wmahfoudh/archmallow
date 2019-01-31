# Backlight adjustment
## Part 1
Check the contents of the folder ``cat /sys/class/backlight/``. In general, you should find a folder for each graphic card.
Mine is Intel and the folder is ``intel_backlight``. On many systems it is ``acpi_video0``

To get the maximum value your system allows for backlight
````console
cat /sys/class/backlight/intel_backlight/max_brightness
````
My Intel graphic card returns ``4539``. To read the current brightness value
````console
cat /sys/class/backlight/intel_backlight/brightness
````
To change the brightness value to 50% for example
````console
echo 2068 > /sys/class/backlight/intel_backlight/brightness
````
The problem with this method is that it needs root privileges
## Part 2
To circumvent the need for root privileges, we can create a ``udev`` rule that the members of the ``video`` group will be allowed to use. Then we add our user to that group

To create the rule, add the following to the ``/etc/udev/rules.d/backlight.rules`` file
````console
ACTION=="add", SUBSYSTEM=="backlight", KERNEL=="intel_backlight", RUN+="/bin/chgrp video /sys/class/backlight/%k/brightness"
ACTION=="add", SUBSYSTEM=="backlight", KERNEL=="intel_backlight", RUN+="/bin/chmod g+w /sys/class/backlight/%k/brightness"
````
Note that in ``KERNEL``, I put the name of the folder of my graphic card found in ``Part 1``, this would change from one configuration to another.

Now, add your user to the group ``video``
````console
usermod -a -G video user_name
````
## Part 3
So far, we solved the privileges problem. But rather than directly editing each time the configuration files we will install a small utility called [brillo](https://gitlab.com/cameronnemo/brillo) to do it more simply. Get it from the AUR by ``yay -S brillo``

``brillo`` can be used this way
````console
# to increase the backlight by 5%
brillo -A 5
# to reduce it by 10%
brillo -U 10
````

For more details on how to use ``brillo``, check its [man page](https://gitlab.com/cameronnemo/brillo/blob/master/doc/man/brillo.1.md). The above commands can be bound to keyboard shortcuts within the window manager later on.
