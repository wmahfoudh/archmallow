# Installing Arch Linux

The rest of this document supposes a wired connection to the internet which I found at this stage, more reliable than a wireless link 

After downloading the Arch Linux ISO file, create a USB boot key. I recommend running ``lsblk`` before and after inserting the USB key and note the new entry which should correspond to that key. A mistake in the drive letter here can cost a disk!
```bash
dd bs=4M if=/path/to/archlinux.iso of=/dev/sdx status=progress && sync
# x being the letter corresponsing to the inserted key
```
Partition disk
```bash
fdisk /dev/sda
# we will create a root, home and swap partitions
```
Create file systems
```bash
# root partition
mkfs.ext4 /dev/sda1
# home partition
mkfs.ext4 /dev/sda3
# swap partition
mkswap /dev/sda2
swapon /dev/sda2
```
Mount the file systems
```bash
mount /dev/sda1 /mnt
mkdir /mnt/home
mount /dev/sda3 /mnt/home
```
Install Arch
```bash
timedatectl set-ntp true
pacstrap /mnt base base-devel
pacman -S intel-ucode
# for Intel processors
```
Generate file system table
```bash
genfstab -U /mnt >> /mnt/etc/fstab
```
Chroot to the new install
```bash
arch-chroot /mnt
```
Create time zone symbolic link
```bash
ln -sf /usr/share/zoneinfo/<Region>/<City> /etc/localtime
```
Generate /etc/adjtime
```bash
hwclock --systohc
```
Localization
```bash
nano /etc/locale.gen
# and uncomment en_US.UTF-8 UTF-8
locale-gen
echo LANG=en_US.UTF-8 > /etc/locale.conf
export LANG=en_US.UTF-8
nano vconsole.conf
# to check keyboard
```
Network
```bash
echo konoha > /etc/hostname
nano /etc/hosts
# fix the hostname previously set
```
Change root password
```bash
passwd
```
Install and configure grub
```bash
pacman -S grub os-prober ntfs-3g exfat-utils
os-prober
grub-install /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
```
Restart
```bash
exit
# exit chroot
umount -R /mnt
umount -R /mnt/home
reboot
```
