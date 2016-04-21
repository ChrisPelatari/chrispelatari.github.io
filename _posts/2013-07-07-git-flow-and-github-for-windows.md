---
layout: post
excerpt: Here's the most recent way I've kept git-flow on my windows 8 machines and up in my life.
---

## what, no getopt?

Every time [github for windows](http://windows.github.com) updates, I lose git-flow. The portable git that is extracted with the install doesn't include getopt.exe, which is needed to install and use git-flow on windows.

## start with the git-flow repository

clone the [git-flow repository](https://github.com/nvie/gitflow)

when you cd to contrib and run msysgit-install.cmd from the cmd line, it says

>MsysGit installation directory not found.
>Try to give the directory name on the command line:
> msysgit-install "C:\Program Files (x86)\Git"

So now you have to find the install directory and try to add that to the msysgit-install cmd line. This time, in my case it was

```
> msysgit-install "C:\Users\Chris\AppData\Local\GitHub\PortableGit_015aa71ef18c047ce8509ffb2f9e4bb0e3e73f13"
> Installing gitflow into "C:\Users\Chris\AppData\Local\GitHub\PortableGit_015aa71ef18c047ce8509ffb2f9e4bb0e3e73f13"...
```

## But wait there's more!

Now it tells us that getopt.exe is not found. Go to the git-flow repository page for [manual install instructions](https://github.com/nvie/gitflow/wiki/Windows) which pretty much outlines the same steps I'm typing right now, so...moving right along

follow the links to [getopt.exe](http://gnuwin32.sourceforge.net/packages/util-linux-ng.htm) and [libintl3](http://gnuwin32.sourceforge.net/packages/libintl.htm) and copy them to your portablegit bin directory. now when you run msysgit-install with the directory parameter, git flow installs. w00t!
