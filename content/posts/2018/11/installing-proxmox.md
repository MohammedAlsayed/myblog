---
title: "Installing Proxmox"
date: 2018-11-24T21:52:02+03:00
draft: true
rtl: false
---

# Introduction

I know that installing proxmox is straight forward. Burning the image on a usb and then booting from the usb from a server or laptop, then follwoing the installation steps. However, unfortunately I tried to do that on my HP pavillion laptop and I was getting a black page with the "GRUB" word in the upper left corner. I tried burning the usb with different softwares and also with different operating systems but the same black page was appearing. So, in this blog I will show you how I solved this issue, and successfully installed proxmox.

# Requirments

- Virtual Box
- USB to SATA cable
- Hard Drive
- Laptop

# Installing proxmox

1- What I did? I first installed a vm proxmox on Virtual Box with:
- vdi hard drive
- 1 core CPU
- 1024 memory

2- After fininshing the installation I cloned the image into a raw format with the VBoxManage CLI. 

    VBoxManage clonehd proxmox.vdi proxmox.img --format RAW

3- Next burned the `proxmox.img` on my hard drive.

