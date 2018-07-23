---
title: "Usefull Linux Cmds"
date: 2018-07-23T13:42:44+03:00
draft: true
rtl: false
---

## Introduction

The following commands I found useful while working. This blog will be updated continuosly.

### sshfs 

This commands syncs a folder in a server with your local directory

    sshfs username@server-ip:/folder/path/in/the/server /local/path
    e.g:
    sshfs root@libvirt:/root/go/src/wirefilter.com/ .

If you finished, you can unmount the folder.
    
    umount -f wirefilter.com

### ssh-copy-id 

Instead of doing the long ssh copy procedure this command does it for you.

    ssh-copy-id username@server-ip
    ssh-copy-id msayed@192.168.100.20

### ssh hostname

Instead of remembring the username and ip address of every server, you can assign it an alias and ssh it with that alias.

open ssh config file:

    vi ~/.ssh/config

add the following config:

    host myserver
	hostname 10.10.10.151
	user msayed

then instead of doing :

    ssh msayed@10.10.10.151
do
 
    ssh myserver

## Forward agent

This is also useful but I don't know how :). I will read about it more.

open ssh config file:

    vi ~/.ssh/config

add the following:

    host *
	    ForwardAgent yes