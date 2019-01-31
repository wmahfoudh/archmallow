## Setting locale
Edit the ``locale.gen`` file to uncomment the needed entries, so ``locale-gen`` can be later be invoked and find entries to add to the system
````console
locale
sudo nano /etc/locale.gen
sudo locale-gen
locale
````
For a list of enabled locales use ``locale -a``. To list available locales which have been previously generated ``localedef --list-archive`` or ``localectl list-locale``

To set the system locale run ``localectl set-locale LANG=en_US.UTF-8`` or add ``LANG=en_US.UTF-8`` to the ``/etc/locale.conf`` file

Source: [Arch Wiki](https://wiki.archlinux.org/index.php/locale)
