---
layout: post
title: "Debian Linux"
description: "how I got up and running with a dual-boot configuration in a day."
category: geek
tags: [debian, linux, ruby, rails, windows]
---

## I have recently been going thru the process of moving some current web properties from asp.net mvc to ruby on rails.

In the past, I have toyed with the idea of moving to rails, enough to get some prototype code running. I feel that the framework has matured quite a bit and it seems like a logical tool to use for rapid, maintainable web development. The last push to go ahead and put some real work into this idea has come with the most recent updates to asp.net. I really like the idea of being able to hack asp.net sites on OS X, and I will see if a transition within .net is doable or desirable in the future. For now tho, if I have to learn a whole new paradigm I might as well learn a new framework while I'm at it. Routing is one area that seems more powerful in rails - mvc routing is very similar and probably as powerful. For now, I want to see how those dirty rails hippies live.

In my quest to learn rails, I needed a dual-boot environment to run alongside windows. I chose debian linux because it seems like it has access to most of the stuff that I need. Debian's installer was pretty impressive. It has a setup.exe that runs from within windows. At first I burned the CD incorrectly (just copied the iso) but after getting that sorted debian installed, put a grub loader in the mbr, and boom I was ready to roll.

After double checking that the dual-boot installed properly, I needed a few tools.

I started with Chromium for the default browser, and then found dropbox and keepass2 and installed those for some xplat love.

+ [Atom editor](http://atom.io)
+ git
+ sudo
+ [rvm](http://rvm.io)
+ bundler

apt-get is the package manager on debian. Atom has a .deb package available for download. I got it installed with dpkg.

```$
dpkg -i atom-amd64.deb
```

ah, but that didn't install all the way. Looking at the logs told me that it was missing git. okay. here is where I started to run into permission problems, so I tried running sudo only to find it not installed by default. :(

it did have su, so I ran under su:

```>
apt-get install sudo
```

now I have sudo, but I'm not listed as a sudoer. So, still under su:

```>
visudo
```

and add the appropriate permissions.

now, I can install git.

```$
sudo apt-get install git
```

git is there. but atom still fails to install. apt-get to the rescue again:

```$
sudo apt-get -f install
```

and that solved it for me.

Next, I needed rvm so I installed it using curl (also not available by default). rvm is very helpful in its messages, so after getting everything sorted there, and restarting the terminal, I could now install and execute bundler. I had to do a couple of extra steps to get postgresql installed locally, adding myself as a user with createdb access. But it worked. In one day.

### I now have windows 7, 10, OS X, and Debian linux installed and I use all of them for development.
