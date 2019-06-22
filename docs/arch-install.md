# Installing Arch Linux

Please refer to the official Arch installation guide [here](https://wiki.archlinux.org/index.php/Installation_guide). The restis by no means a replacement, it's just personal notes 

Flashing the ISO to a USB key
```bash
dd bs=4M if=/path/to/archlinux.iso of=/dev/sdx status=progress && sync
# x being the letter corresponsing to the inserted key
```
Partitioning the disk (GPT)
```bash
fdisk /dev/sda
# sda1 EFI 512M
# sda3 Linux swap (size 2xRAM)
# sda2 Linux FS to mount root (size = remaining space)
```
Creating file systems
```bash
# EFI partition
mkfs.fat -F32 /dev/sda1
# root partition
mkfs.ext4 /dev/sda2
# swap partition
mkswap /dev/sda3
swapon /dev/sda3
```
Mount the file systems
```bash
mount /dev/sda2 /mnt
mkdir /mnt/efi
mount /dev/sda1 /mnt/efi
```
Install Arch
```bash
timedatectl set-ntp true
pacstrap /mnt base base-devel
```
Generate file system table
```bash
genfstab -U /mnt >> /mnt/etc/fstab
```
Chroot to the new install
```bash
arch-chroot /mnt
pacman -S intel-ucode
# for Intel processors
```
Network
```bash
echo konoha > /etc/hostname
nano /etc/hosts
127.0.0.1	localhost
::1		localhost
127.0.1.1	konoha.workgroup	konoha
```
Change root password
```bash
passwd
```
Install and configure grub
```bash
pacman -S grub os-prober ntfs-3g exfat-utils
os-prober
grub-install --target=x86_64-efi --efi-directory=/efi
grub-mkconfig -o /boot/grub/grub.cfg
```
Restart
```bash
exit
# exit chroot
umount -R /mnt/efi
umount -R /mnt
reboot
```
