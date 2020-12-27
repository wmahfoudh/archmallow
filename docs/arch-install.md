# Installing Arch Linux

Please refer to the official Arch installation guide [here](https://wiki.archlinux.org/index.php/Installation_guide). The rest is by no means a replacement of the wiki, just personal notes 

Flashing the ISO to a USB key
```bash
dd bs=4M if=path/to/archlinux.iso of=/dev/sdx status=progress oflag=sync
```
Partitioning the disk (GPT)
```bash
fdisk /dev/sda
# sda1 EFI 256M
# sda2 Linux swap (size 2xRAM)
# sda3 home partition
# sda4 Linux FS to mount root (size = remaining space)

```
Creating file systems
```bash
# EFI partition
mkfs.fat -F32 /dev/sda1
# swap partition
mkswap /dev/sda2
swapon /dev/sda2
# home partition
mkfs.ext4 /dev/sda3
# root partition
mkfs.ext4 /dev/sda4
```
Mount the file systems
```bash
# mounting the root partition
mount /dev/sda4 /mnt
# mounting the efi partition
mkdir /mnt/boot
mkdir /mnt/boot/efi
mount /dev/sda1 /mnt/boot/efi
# mounting the home partition
mkdir /mnt/home
mount /dev/sda3 /mnt/home
```
Install Arch
```bash
timedatectl set-ntp true
pacstrap /mnt base linux linux-firmware base-devel nano networkmanager man-db man-pages texinfo
```
Generate file system table
```bash
genfstab -U /mnt >> /mnt/etc/fstab
```
Chroot to the new installation
```bash
arch-chroot /mnt
```
Network configuration
```bash
echo akatsuki > /etc/hostname
nano /etc/hosts
127.0.0.1	localhost
::1		localhost
127.0.0.1	akatsuki.workgroup	akatsuki
```
Change root password
```bash
passwd
```
Time zone and locale
```bash
ln -sf /usr/share/zoneinfo/Asia/Dubai /etc/localtime
hwclock --systohc
nano /etc/locale.gen
# uncomment needed locales, save and run locale-gen
locale-gen
```
Install and configure grub
```bash
pacman -S grub os-prober ntfs-3g exfat-utils intel-ucode
os-prober
grub-install --target=x86_64-efi --efi-directory=/boot/efi
grub-mkconfig -o /boot/grub/grub.cfg
```
NetworkManager
```bash
systemctl enable NetworkManager.service
systemctl start NetworkManager.service
```
Restart
```bash
exit
# exit chroot
umount -R /mnt/efi
umount -R /mnt
reboot
```
