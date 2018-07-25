---
title: "Backing Up Server"
date: 2018-07-25T16:33:47+03:00
draft: true
rtl: false
---

    sudo rsync -aAXv / --exclude={"/dev/*","/proc/*","/sys/*","/tmp/*","/run/*","/mnt/*","/media/*","/lost+found"}

To restore substitute the source and destination