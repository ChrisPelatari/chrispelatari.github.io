---
layout: post
title: "Running 1Password on Debian Linux"
description: "How I got 1Password for Windows running on Debian Linux"
category: geek
tags: [geek]
---

## This is how I got 1Password for Windows v4.6.0.604 running on Debian Linux

The first thing I tried was just running the installer with wine at the terminal.

```
chris@Callisto:~/Downloads$ wine 1Password-4.6.0.604.exe
wine: Bad EXE format for Z:\home\chris\Downloads\1Password-4.6.0.604.exe.
```

Well crap. what does that mean? Could the 1Password installer be 32bit, while my system is 64? Bingo. You won't find that info on the [official AgileBits walkthrough](https://support.1password.com/1password-in-wine/).

So instead of using the terminal, I turned to PlayOnLinux, which gives more options for installation.

I don't know if this was a requirement, but I chose wine version 1.4.1 in PlayOnLinux, also the 32 bit installation. Browsed the 1Password.4.6.0.604.exe file and ran the installer like normal. It even accepted my license key.

#### Now I have a working 1Password installation on my Debian Linux machine

hth
