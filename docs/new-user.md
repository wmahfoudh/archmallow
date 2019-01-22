Before creating a new user, it would be a good idea to create a password for the **root** user by typing the `passwd` command while logged-in as root (which should be the case if you have a fresh install)
# Creating a new user
````bash
useradd -m -G wheel -s /bin/bash username
# create a new user and add it to the wheel group
passwd username
# create a password for the newly created user
````
Installing sudo package
````bash
pacman -Syu sudo
````
Configuring sudo to allow the wheel group member to use it
````bash
visudo
# visudo is an editor for the sudo config file
# which verifies it before saving
````
Look for the following line
````bash
# %wheel ALL=(ALL) ALL
````
Uncomment that line by placing the cursor on the # and pressing x (which in vi editor deletes the caracter). To save and quit *visudo* type **:wq**
