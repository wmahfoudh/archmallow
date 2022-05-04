# Useful Pacman commands
Sync DB
````bash
pacman -Sy
````
Force sync DB (case of a repository change for example)
````bash
pacman -Syy
````
System update (not recommended because without DB sync)
````bash
pacman -Su
````
System update (recommended)
````bash
pacman -Syu
````
Download a package without installation
````bash
pacman -Sw package_name
````
Install a downloaded or a local package
````bash
pacman -U /package_path/package_name.pkg.tar.xz
pacman -U http://www.examplepackage/repo/examplepkg.tar.xz
# list cached packages
ls /var/cache/pacman/pkg | grep linux
````
Reinstall all packages
````bash
pacman -Syu $(pacman -Qqen)
````
Remove a package
````bash
pacman -R package_name
````
Remove a package along with its non used deps (typical use)
````bash
pacman -Rs package_name
````
Remove a package with all deps (even used ones, not recommended)
````bash
pacman -Rsc package_name
````
Remove a package with its config files
````bash
pacman -Rn package_name
````
Remove a package with all deps (even used ones) and config files
````bash
pacman -Rscn package_name
````
Remove dependencies leaving package
````bash
pacman -Rdd package_name
````
Cache clean
````bash
pacman -Sc
````
Cache clean, remove all packages (no downgrade)
````bash
pacman -Scc
````
Cleaning orphan packages
````bash
pacman -Rsn $(pacman -Qdtq)
````
Search a package
````bash
pacman -Ss package_name
````
Search a package in installed ones
````bash
pacman -Qs package_name
````
Detailed summary of a package
````bash
pacman -Si package_name
# or
pacman -Qi package_name
````
Installed packages
````bash
pacman -Q
````
Find out which package owns a file
````bash
pacman -Qo /file_path
````
List all orphan packages with no dependencies
````bash
pacman -Qdt
````
List all installed packages from the AUR
````bash
pacman -Qem
````
View package dependencies
````bash
pactree package_name
pactree -c package_name
pactree -s -c package_name
````
Get full packages list
````bash
pacman -Q > ~/pacman.list
````
# Fixing invalid or corrupted package problem (PGP signature)
This usually happens when system is not maintained for long, PGP keys get obsolete, they need to be updated 
````bash
pacman -Sy archlinux-keyring
pacman-key --populate archlinux
pacman-key --refresh-keys
pacman -Syu
````
When the system is not maintaned for long, chances are some dependencies need to be ignored and defult options forced to avoid confirmation
````bash
pacman -Syu -d --noconfirm
````
