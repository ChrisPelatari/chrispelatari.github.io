---
layout: post
title: Dual booting Linux Redhat 9 and Windows XP using a CD
date: 2005-08-26 14:45
author: chrispelatari
comments: true
categories: [professional_geek]
---

<p>We have a couple of legacy applications here, written in C++, that have 
always run on windows and *nix. In order to support the *nix versions, we always 
have to have a Linux install hanging around (we also have a solaris, but that's 
already set up).</p>
<p>So we got a Dell Precision 380 workstation with a SATA drive that had Windows 
XP installed on it. Since the Dell didn't come with a floppy drive, I couldn't 
very well just create a boot diskette. That would be useless. So based on the 
fact that there is a spec called "El Torito", I looked up an <a href="http://url123.com/ucrup">article online about Linux Bootdisks</a>. It 
looked pretty good, but there was one glaring omission: the author mentions that 
you need to load any initial ramdisk via LILO, but doesn't explain how to setup 
LILO correctly for a floppy image. I decided to go back to it if necessary and 
went to redhat.com to see if there was any insight there.</p>
<p>I ended up finding a section of documentation that outlines <a href="http://url123.com/uc6sh">how to create an Installation Boot CD-ROM</a>, 
but I had already installed it! I later found that if at the bootloader screen 
of the install CD I typed the command:</p><pre>vmlinuz root=/dev/hdb2</pre>
<p>It would in fact load the installation off of the second (IDE) harddrive 
(thanks, btw, linux for making me use a modified kernel to support SATA drives. 
That's top-notch, guys.)</p>
<p>So I figured that the secret to the sauce was probably in the isolinux.cfg 
file that configures all the commands visible at the boot loader screen. First I 
tried something like this: </p><pre><span style="color:blue;">default</span> linux
label linux
	kernel vmlinuz
	append root=/dev/hdb2 initrd=initrd.img</pre>
<p>but that didn't work, it still brings up the install screen. So I figured why 
not try the simplest possible solution using the config file, and this is what I 
came up with:</p><pre><span style="color:blue;">default</span> vmlinuz root=/dev/hdb2</pre>
<p>Guess what? I now have a Redhat Linux 9 install that will boot from a CD and 
I didn't have to mess with a bootmanager or touch the MBR in any way. I don't 
have to wait those pesky 10 seconds for either grub or the windows NT bootloader 
to select which install to start - I just pop in a CD if I want linux, and open 
it if I want WinXP.</p>
