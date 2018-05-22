---
layout: post
title: "github for windows and babun"
categories: [git,zsh]
---
If you are on windows 10, you can simply use a linux subsystem. That ain’t what we’re talmbout here.

[babun](http://babun.github.io/) is a cygwin based shell with a bunch of defaults added that aren't included with the portablegit install that comes with [github for windows](https://desktop.github.com). Some of those defaults that I wanted to include, indeed what pushed me to try babun, are zsh and [oh-my-zsh](http://ohmyz.sh/). (I was tryna figure out a way to include it in the portablegit, but ran into some roadblocks, such as no autoconf)

Setting up a custom shell in g4w is pretty straightforward, just open up options... and  add the following to the Custom selection for Default Shell:

```
C:\Users\<username>\.babun\babun.bat
```

That's it!

I also added [powerlevel9k](https://github.com/bhilburn/powerlevel9k) and [zsh-syntax-highlighing](https://github.com/zsh-users/zsh-syntax-highlighting), using the [Inconsolata for Powerline font](https://github.com/powerline/fonts/tree/master/Inconsolata)
