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
# Using the same device with more than a system (dual boot, etc.)
Once paired, authentication keys are stored in the host computer and in the device itself.
Most bluetooth devices can manage only one authentication key. So if you pair your device with a Linux computer, and want to use it in Windows, you need to pair it again.

A workaround is to pair the device on Linux, switch to windows, pair the device again and then copy the Windows authentication key to Linux. The opposite is also possible.

On Arch, the authentication keys are stored in ``/var/lib/bluetooth/controller_mac/`` and the mouse keys in ``/var/lib/bluetooth/controller_mac/mouse_mac/``. The key is in the ``[LinkKey]`` section:
````console
[LinkKey]
Key=F51BBFA0490561B8A87E62A7670A8D99
````

On Windows, the keys are stored in the registry ``LOCAL_MACHINE\CurrentControlSet\services\BTHPORT\Parameters\Keys`` just followed by the mac address of the device. If no ``CurrentControlSet`` try ``Controlset001`` an so on.

This technique works on Windows with Microsoft bluetooth stack, some vendors like Toshiba have their own stack, and the authentication keys are not stored in the registry (Toshiba stores them in a local encrypted database). 

For more details see [here](http://console.systems/2014/09/how-to-pair-low-energy-le-bluetooth.html) and [here](https://unix.stackexchange.com/questions/255509/bluetooth-pairing-on-dual-boot-of-windows-linux-mint-ubuntu-stop-having-to-p).
