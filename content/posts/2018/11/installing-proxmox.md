---
title: "Installing Proxmox"
date: 2018-11-24T21:52:02+03:00
draft: false
rtl: false
---

## Introduction

I know that installing proxmox is straight forward. First, burning the image on a usb and then booting from a server or laptop , then follwoing the installation steps. Unfortunately, I tried to do that on my HP pavillion laptop and I was getting a black page with "GRUB" word appering in the upper left corner. I tried burning the usb with different softwares and also with different operating systems but the same black page was appearing. So, in this blog I will show you how I solved this issue, and successfully installed proxmox.

## Requirments

- [Virtual Box](https://www.virtualbox.org/wiki/Downloads)
- [USB to SATA cable](https://www.amazon.com/StarTech-com-SATA-Drive-Adapter-Cable/dp/B00HJZJI84)
- Hard Drive
- Laptop

## Solving the issue

1- What I did? I first installed a vm proxmox on Virtual Box with the following specfications:

- vdi hard drive
- 1 core CPU
- 1024 memory

2- After fininshing the installation I cloned the image into a raw format with the VBoxManage CLI. 

    VBoxManage clonehd proxmox.vdi proxmox.img --format RAW

3- Next burned the `proxmox.img` on my hard drive with `dd`. Here is how:

- Finded the hard drive name thru `diskutil list`. Which is /dev/disk2
- Formated the disk `diskutil eraseDisk FREE pve /dev/disk2`
- Then purned proxmox to the hard drive `sudo dd if=proxmox.img of=/dev/disk2`

4- Connected the hard drive to my laptop and finally it worked!. But now I faced an issue with the volume sizes which where too small according to my sda 750GB hard drive. Specially the two logical volumes: `pve-root` = 1.8GB which contains the iso files and `pve-data`=2.3GB which will have the VMs data . 

    root@home-vm:~# lsblk
    NAME               MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
    sda                  8:0    0 698.7G  0 disk 
    ├─sda1               8:1    0     1M  0 part 
    ├─sda2               8:2    0   256M  0 part 
    └─sda3               8:3    0   7.8G  0 part 
    ├─pve-swap         253:0    0   896M  0 lvm  [SWAP]
    ├─pve-root         253:1    0   1.8G  0 lvm  /
    ├─pve-data_tmeta   253:2    0     1G  0 lvm  
    │ └─pve-data       253:4    0   2.3G  0 lvm  
    └─pve-data_tdata   253:3    0   2.3G  0 lvm  
        └─pve-data     253:4    0   2.3G  0 lvm  

To increase there size, enter the console of the proxmox and do the following:

    apt-get install parted
    parted /dev/sda 
    
    (parted) print
    Warning: Not all of the space available to /dev/vda appears to be used, you can
    fix the GPT to use all of the space (an extra 1448371952 blocks) or continue
    with the current setting? 
    Fix/Ignore? F 

    resizepart 3 100%
    quit

Now `sda3` free size is larger 

    fdisk -l /dev/sda | grep ^/dev

    /dev/sda1    2048       4095       2048     1M BIOS boot
    /dev/sda2    4096     528383     524288   256M EFI System
    /dev/sda3  528384 1465149134 1464620751 698.4G Linux LVM

before:

    fdisk -l /dev/sda | grep ^/dev

    /dev/sda1    2048     4095     2048    1M BIOS boot
    /dev/sda2    4096   528383   524288  256M EFI System
    /dev/sda3  528384 16777182 16248799  7.8G Linux LVM

Then after increasing the hard drive, increase the logical volumes:

    lvresize --size +40G --resizefs /dev/pve/root
    lvresize --size +5G --resizefs /dev/pve/swap
    lvresize --size +200G --resizefs /dev/pve/data

    root@home-vm:~# lsblk

    ├─pve-swap                     253:0    0   5.9G  0 lvm  [SWAP]
    ├─pve-root                     253:1    0  41.8G  0 lvm  /
    ....
        ├─pve-data                 253:5    0 202.3G  0 lvm  

Finally `pve-swap`, `pve-root`, `pve-data` LVS increased