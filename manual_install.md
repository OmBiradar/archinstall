# Manual Install

Setting up hyperland arch linux from scratch

_Table Of Contents_

1. Download ISO from Arch Linux website - 10 min
2. Burn the ISO - 5 min
3. Boot up Arch Linux

## 1. Download ISO form Arch Linux website

Go to https://archlinux.org/download/, scroll down to your country/ nearest country and download the ISO.

Download the latest version from the fastest server.

## 2. Burn the ISO

Download and install BalenaEtcher from https://etcher.balena.io/#download-etcher

Get a PenDrive and use the downloaded ISO with Etcher to burn the ISO in the PenDrive

## 3. Boot up Arch Linux

Setup your keyboard layout, for english

```
loadkeys us
```

To connect to the internet, use iwctl,

```
iwctl
device list
device wlan0 connect <SSID>
```

Test your internet connection with

```
ping google.com
```

Now partition your disk, to list the disks,

```
lsblk
```

then to format the disks, use

```
fdisk
```

create 3 main partitions

- 100 MB boot
- 16 GB swap
- Remining storage for root storage

use mkfs commands to format the partitions into the correct type

```
# For root
mkfs.ext4 /dev/sda3

# For boot
mkfs.fat -F 32 /dev/sda1

# For swap
mkswap /dev/sda2
```

Now mount your root partition, make the boot partition point, turn the swap on,

```
mount /dev/sda3 /mnt
mkdir -p /mnt/boot/efi
mount  /dev/sda1 /mnt/boot/efi
swapon /dev/sda2
```

Install required packages into the root by,

```
pacstrap /mnt base linux linux-firmware sof-firmware base-devel grub efibootmgr nano vim nvim networkmanager
```

Generate the file system

```
genfstab /mnt > /mnt/etc/fstab
```

Now, setup the system from the inside,

```
arch-chroot /mnt

# Setup local time zone
ln -sf /usr/share/zoneinfo/Asia/Kolkata /etc/localtime
date # To confirm
hwclock --systohc # Synchronize the system clock

# Localization
nano /etc/locale.gen # uncomment the line "en_US.UTF-8 UTF-8"
locale-gen
nano /etc/locale.conf # Write "LANG=en_US.UTF-8"

# Hostname
nano /etc/hostname # Write your machine hostname (can be capital letters also!)
passwd # Set the host password
useradd -m -G wheel -s /bin/bash <username>
passwd <username> # set the user password
su <username>
EDITOR=nano visudo # Uncomment the line "%wheel ALL=(ALL) ALL
su <username>

# Enable Services
systemctl enable NetworkManger

# Setup GRUB
grub-install /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
exit

# Unmount and reboot
umount -a
reboot
```

Now setup arch linux

Log into your user
quick tip - to double your font, use `setfont -d`

Install a graphical environment, we will go with hyperland

```
sudo pacman -S plasma sddm
sudo systemctl enable --now sddm
```

And you are done!

> Additionally I found that installing some more software was usefull and is covered in this sectiton
