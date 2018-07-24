---
title: "Cloudinit and Virtualbox"
date: 2018-07-24T17:03:47+03:00
draft: false
rtl: false
---

# Introduction

You should have an image that contains cloudinit:

- There are ready made images that can be found [here](https://cloud.centos.org/centos/7/images/), chose images that have GenericCloud

- Or you can create you own image by following this [tutorial](https://docs.openstack.org/image-guide/create-images-manually.html)

## Steps 

1- first create your meta data, user data files

user data file:

    #cloud-config
    password: mypassword
    chpasswd: { expire: False }
    ssh_pwauth: True
    ssh_authorized_keys:
        - <paste your ssh pub key>

meta data file:

    instance-id: 1
    local-hostname: myserver-name

2- Then generate an iso image (will be used as CD)

    genisoimage -output init-cidata.iso -volid cidata -joliet -rock user-data meta-data

Now attach this cd to the vm, as in the figure

![vm-cd](/img/2018/7/vm-cd.png)

And thats it. Just start your server ! 
Then ssh to your server if you know its ip address :).
If your server is on NAT you can create forwarding a port form the settings -> network -> advanced -> port forwarding. Then add the following:

![nat-ssh](/img/2018/7/nat-ssh.png)

Now 

    ssh -p 9090 centos@localhost 

centos is the default user created. You can change that if you [want](https://cloudinit.readthedocs.io/en/latest/topics/examples.html)

