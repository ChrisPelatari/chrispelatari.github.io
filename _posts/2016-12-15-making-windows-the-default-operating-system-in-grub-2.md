---
title: "Making Windows the default operating system in grub 2"
layout: post
author: chrispelatari
categories: [Windows, grub, linux]
---

tl;dr: change GRUB_DEFAULT=0 to the zero-based index of the Windows entry in the grub config file.

Windows updates seem to be happening at least once a week these days. Most of the time, the updates require a reboot to finish. I just happen to be running Debian linux on the same machine, which uses grub 2 to load each OS installed on the system. The default OS loaded is the first one in the list, in my case Debian. So, if I have to reboot my Windows install and walk away from my computer, I return to a Debian login screen. Well, this was true up until now.

I started with the suggestion [to edit the grub file here](https://www.danbishop.org/2011/05/26/make-windows-the-default-operating-system-in-grub2-even-after-ubuntu-updates/)

However, this didn't work for me...instead of Vista as indicated in the link above, I have Windows 7 installed so the entry in grub is Windows 7 (loader) on dev/sda1 so I tried this as a replacement:

```
GRUB_DEFAULT="Windows 7 (loader) on dev/sda1"
```

(I use vi to edit files on linux:)

```
$ vi /etc/default/grub
```

After rebooting the system, without changing the grub menu position, I was presented with the Debian login screen again.

Well shit.

So I decided to use the zero-based index of the OS this time...because the default is 0, with Windows being the third entry in the grub loader, I changed the default to 2:

```
GRUB_DEFAULT=2
```

After a sudo update-grub, and another sudo reboot, without touching the grub menu, I sat back and watched as Windows was loaded by default from grub.

Success!
