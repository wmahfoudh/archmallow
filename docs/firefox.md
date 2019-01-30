## Installation
````console
sudo pacman -S firefox flashplugin
````
Ensure you install the fonts discribed in [Utilities](./utilities.md)
## about:config tweaks
- set ``dom.ipc.processCount`` to ``7``
- set ``browser.preferences.defaultPerformanceSettings.enabled`` to ``False``
- set ``layers.acceleration.force-enabled`` to ``True`
- Create a new boolean value named ``gfx.canvas.azure.accelerated`` and set it to ``True``
- Disable pocket by setting ``extensions.pocket.enabled`` to ``False``
- Set ``network.protocol-handler.expose.magnet`` to ``False``. In case it does not exist create it

Source : [Arch wiki: Tweaks/Firefox](https://wiki.archlinux.org/index.php/Firefox/Tweaks#Jerky_or_choppy_scrolling)
