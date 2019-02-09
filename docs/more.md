# More useful stuff
The installation discribed in previous steps provides a "minimal and working system", here are few other tools, for more specific use
## dvgrab
For capturing viseo and audio from FireWire cameras (IEEE 1394), you need ``dvgrab``

Install it with ``sudo pacman -S dvgrab``. A typical use would be

````bash
dvgrab --autosplit --timestamp --size 0 --rewind FilesName-
````
## python-pip
If you're a Python programmer you would need PyPA recommended tool for installing Python packages
````bash
sudo pacman -S python-pip
````
## Thunar
[Thunar](https://wiki.archlinux.org/index.php/Thunar) is a lightweight files manager, it can automount removable drives if started as a deamon at login ``thunar --daemon``
````bash
sudo pacman -S thunar thunar-archive-plugin thunar-media-tags-plugin thunar-volman
````
