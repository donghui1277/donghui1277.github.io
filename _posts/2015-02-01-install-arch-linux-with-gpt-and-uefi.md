---
layout: post
title: "Install Arch Linux With GPT And UEFI"
description: 
headline: 
modified: 2015-02-01
category: personal
tags: [linux]
image: 
  feature: 
comments: true
mathjax: 
---

#说明
在笔记本真机上安装Arch Linux已经是几个月前的事情了，当时刚买了固态硬盘，就把原来的硬盘用来安装了Arch Linux。
[官方论坛的安装指南](https://wiki.archlinux.org/index.php/Installation_guide)已经够详细了，但第一次安装，还是遇到了一些问题。所以记录一下，备忘。

#安装纯系统
分区:使用了cfdisk，为了简化安装，分了两个分区，主分区和交换分区。<br/>

注意：由于使用了GPT + UEFI，需要事先分好EFI分区 sda1 fat格式。<br/>
主分区sda2设置为bootabl，swap分区为sda3

格式化mkfs.ext4 /dev/sda1

创建swap分区：`mkswap /dev/sda3`<br/>
启用swap分区：`swapon /dev/sda3`

挂载主分区 `mount /dev/sda2 /mnt`

建立efi目录，把EFI分区装载到刚建立的efi目录上。

	# mkdir -p /mnt/boot/efi
	# mount /dev/sda1 /mnt/boot/efi

打开mirrorlist文件，把中国的镜像服务器地址放到前面。编辑器可以选nano或是vi。

    # vi /etc/pacman.d/mirrorlist

切换到挂载的主分区上，建立分区表

    # pacstrap /mnt base
    # genfstab -p /mnt >> /mnt/etc/fstab
    # arch-chroot /mnt

设置主机名和时区

    #echo computer_name > /etc/hostname
    #locale-gen
    #ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

基本系统配置：<br/>
1）修改编码

    #vi /etc/locale.gen
    
    en_US.UTF-8 UTF-8
    zh_CN.UTF-8 UTF-8
    zh_TW.UTF-8 UTF-8

应用更改：

    # locale-gen

2) 修改本地语言：

    # echo LANG=en_US.UTF-8 > /etc/locale.conf 
    

3）设置时区

    # ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
    
4）设置硬件时间

    # hwclock --systohc --utc
    
5）设置网络

    # systemctl enable dhcpcd.service
    # mkinitcpio -p linux

6）设置root密码，完成安装

    # passwd
    
7）GRUB启动, UEFI的系统，要装grub-efi-x86_64和efibootmgr

    #pacman -S grub-efi-x86_64, efibootmgr
    
8）把GRUB装到EFI分区里，这样就多一条GRUB启动项了

    #grub-install --efi-directory=/boot/efi --bootloader-id=arch-grub --recheck
    # grub-mkconfig -o /boot/grub/grub.cfg
    
9）添加一个普通用户
    # useradd -m -g users -G audio,video,floppy,network,rfkill,scanner,storage,optical,power,wheel,uucp -s /usr/bin/bash username
    # passwd username


#安装xfce4和slim
    pacman -S xorg-server xorg-xinit xorg-utils xorg-server-utils
    pacman -S xfce4

安装其他驱动程序

    #pacman -S xf86-video-ati xf86-input-mouse xf86-input-keyboard xf86-input-evdev xf86-input-synaptics
    #pacman -S laptop-mode-tools ntfs-3g dvd+rw-tools

安装字体

    #pacman -S ttf-arphic-uming ttf-arphic-ukai ttf-dejavu wqy-zenhei wqy-microhei

安装Xorg

    #pacman -S xorg-server xorg-xinit xorg-utils xorg-server-utils

安装SLim

    #pacman -S slim
    #systemctl enable slim.service
    #vi /etc/slim.conf //编辑slim配置文件，将session设为startxfce4

安装Xfce4

    #pacman -S xfce4 xfce4-goodies systemd-sysvcompat
    #cp /etc/skel/.xinitrc ~
    #vi ~/.xinitrc //编辑xinitrc,写入exec startxfce4
    #chmod +x ~/.xinitrc
