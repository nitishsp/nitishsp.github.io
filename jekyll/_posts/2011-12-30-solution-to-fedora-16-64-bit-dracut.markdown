---
layout: post
title: "Solution to Fedora 16 (64-bit) Dracut problem"
external_url: http://nitishsp.blogspot.in/2011/12/solution-to-fedora-16-64-bit-dracut.html
---

I had been using Fedora 14 before I decided to switch to Fedora 16. So I downloaded 64-bit iso and created a live usb media using [Live USB Creator](https://fedorahosted.org/liveusb-creator/). When I tried to boot off the usb, I got the following error:

    dracut Warning: No root device "live:/dev/disk/by-uuid/FOEC-AD4C" found.
    dropping to debug shell.
    sh: can't access tty; Job control turned off
    dracut:/#

I found a lot of people getting the same error with no thread/post pointing to the exact solution. Finally I came across [solution to a similar problem](http://www.fedoraforum.org/forum/showpost.php?p=1476942&postcount=3) thanks to [kylerconway](http://www.fedoraforum.org/forum/member.php?u=183341) on fedoraforums.

The solution is quite simple,

1. In the debug shell, type `ls -l /dev/disk/by-uuid/` to find UUID of your boot media. (you may run `ls -l /dev/disk/by-label/` to get better understanding of your disk drives)
2. Once you have UUID of your boot media, reboot and edit GRUB boot command & replace existing UUID with the one found in step 1.

Fedora 16 with GNOME 3.2 looks brilliant (I switched from F14). Also, after using it for a while I found it less buggy. If you are still using Fedora 14, I guess its the right time to switch!

![Fedora 16](http://1.bp.blogspot.com/-PkAu-S4cUq0/Tv3jvyebVjI/AAAAAAAAAVM/wUW1LnzolRU/s640/Screenshot+at+2011-12-10+23%253A01%253A23.png)