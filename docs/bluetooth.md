# Installation
We need to install the needed packages and setup the service
````console
sudo pacman -S bluez bluez-utils pulseaudio-bluetooth
systemctl enable bluetooth.service
systemctl staraliast bluetooth.service
````
Then edit the configuration file ``/etc/bluetooth/main.conf`` to play with some options. You can for instance set the various timeouts.
I recommen though to set ``AutoEnable=true``, this will ensure all controllers are enabled once discovered, even those hot plugged
# Connections
To connect a device, you need to run ``bluetoothctl`` and type the following commands which are self explanatory
````console
power on
agent on
default-agent
pairable on
scan on
````
Upon the scan request, ``bluetoothctl`` will return a set of mac addresses of nearby devices.
Copy the one you're interested in, ``01:02:03:04:05:06`` for example and run
````console
trust 01:02:03:04:05:06
pair 01:02:03:04:05:06
connect 01:02:03:04:05:06
````
The device will be recognized, unblock it
````console
[Microsoft Sculpt Comfort Mouse]# unblock
````
# Solving the dual boot problem
Once paired, authentication keys are stored in the host computer as weel as in the device itself.
Most bluetooth devices can manage only one authentication key. So if you pair your device with a Linux computer, and want to use it in Windows 
