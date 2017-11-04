# arch installation
## instructions on how to setup arch linux ![](https://www.archlinux.org/static/logos/archlinux-logo-dark-1200dpi.b42bd35d5916.png)

- check internet connection (use wired to make it easy)

  `ping -c 3 google.com` 

- update pacman database

  `pacman -Syy`

- install a reflector

  `pacman -S reflector`

- setup reflector

  `reflector -c "US" -f 12 -l 10 -n 12 --save /etc/pacman.d/mirrorlist`

- check for partitions

  `fdisk -l`

- repartition hard drive (erase all partitions make one that takes up the whole disk, make it the primary partition, then make it bootable. Write the changes. 

  `cfdisk` (location of hard drive)

- Format the disk to ext4

  `mkfs.ext4` (location of disk with partition number)

- format swap partition

  `mkswap` (location of swap with partition number)

  `swapon` (location of swap with partition number)

- mount disk to system 

  `mount` (disk location with partition number) `/mnt`

- install base system 

  `pacstrap -i /mnt base base-devel`

- generate fstab file

  `genfstab -U -p /mnt >> /mnt/etc/fstab`

- login to new system as root 

  `arch-chroot /mnt /bin/bash`

- set location of system (uncomment en_US.UTF-8 UTF-8)

  `nano /etc/locale.gen` 

- generate local

  `locale-gen`

- set the clock (replace US and Mountain if you aren't in the mountain time zone)

  `ln -sf /usr/share/zoneoinfo/US/Mountain /etc/localtime`

  `hwclock --systohc --utc`

- give computer a name

  `echo (computer name) > /etc/hostname`

- edit host file add 127.0.1.1 to ipaddress, localhost.localdomain to hostmane.domain.ort, and pc name to hostname

  `nano /etc/hosts`

- enable network service
  
  `systemctl enable dhcpcd`

- set password for root

  `passwd`

- install the bootloader grub

  `pacman -S grub`

- install grub bootloader to hdd

  `grub-install` (location of hard drive)

- generate configuration file

  `grub-mkconfig -o /boot/grub/grub.cfg`

- logout of the system

  `exit`

- unmount the system

  `umount -R /mnt`

- reboot take disk or usb out of the computer

  `reboot`

- log into root using the password you set 

- create a new user

  `useradd -m -g users -G wheel -s /bin/bash (username)`

- assign a password to user

  `passwd` (username)

- add new user to sudo group (uncomment %wheel ALL=(ALL) ALL)

  `EDITOR=nano visudo`

- logout of root

  `exit` 

- login as new user 

- install audio packages

  `sudo pacman -S pulseaudio pulseaudio-alsa`

- install xorg server (leave the first option the default, the second one need to be 1 if you're using integrated graphics)

  `sudo pacman xorg -S xorg xorg-xinit`

- create file of initiation for GUI


  `echo "(gui of choice)" > ~/.xinitrc`

  `sudo pacman -S gnome`

---
xfce:
"exec startxfce4"
`sudo pacman -S xfce4`

gnome:
"exec gnome-session"
`sudo pacman -S gnome`

cinnamon:
"exec cinnamon-session"
`sudo pacman -S cinnamon`

mate:
"exec mate-session"
`sudo pacman -S mate`

unity:
"exec unity"
Unity installation is tricky - see https://wiki.archlinux.org/index.php/...

openbox:
"exec openbox-session"
`sudo pacman -S openbox`

i3:
"exec i3"
`sudo pacman -S i3`

awesome:
"exec awesome"
`sudo pacman -S awesome`

deepin
"exec startdde"
`sudo pacman -S deepin`

LXDE
"exec startlxde"
`sudo pacman -S lxde`

---
- install aditional packages like a file manager, terminal inulater, web browser, and text editor

  `sudo pacman -S konsole dolphin firefox kate`

- start gui

  `startx﻿` 


troubleshooting
======

- if gnome-terminal doesn't work use this command

  `localectl set-locale LANG="en_US.UTF-8"`

  `locale-gen`

  `reboot`

---
- to enable network settings

  `systemctl start NetworkManager.service`

  `systemctl enable NetworkManager.service`

---
- to troubleshoot virtualbox

  `sudo pacman -S virtualbox-host-modules-arch`

  (installs modules)

  `sudo modprobe vboxdrv vboxnetadp vboxnetflt vboxpci`

  `reboot`

---
- enable login manager(GDM comes preinstalled)

  `systemctl enable gdm.service`

  `reboot`



