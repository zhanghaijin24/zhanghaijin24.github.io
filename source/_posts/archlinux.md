---
title: archlinux
---

# 安装archlinux
---
- timedatectl set-ntp true

*#fdisk /dev/sda*
![B12B5CA3-B572-46EE-B998-595DD82F79BE.jpg](http://101.201.197.193/images/2021/01/06/B12B5CA3-B572-46EE-B998-595DD82F79BE.jpg)
![D242AF9D-6380-4167-B834-4BFC420E927D.jpg](http://101.201.197.193/images/2021/01/06/D242AF9D-6380-4167-B834-4BFC420E927D.jpg)
*fdisk -l*

- mkfs.fat -F32 /dev/sda1

- mkfs.ext4 /dev/sda3

- mkswap /dev/sda2
- swapon /dev/sda2

- mount /dev/sda3 /mnt
- mkdir -p /mnt/boot/efi
- mount /dev/sda1 /mnt/boot/efi

- pacstrap /mnt base linux linux-firmware

***vim /etc/pacman.d/mirrorlist***
```
##China
Server = http://mirrors.163.com/archlinux/$repo/os/$arch
```


