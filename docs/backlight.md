# Backlight adjustment
## Method 1
Check the contents of the folder ``cat /sys/class/backlight/``. In general, you should find a folder for each graphic card.
Mine is Intel and the folder is ``intel_backlight``, on many systems it is ``acpi_video0``
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
## Method 2
