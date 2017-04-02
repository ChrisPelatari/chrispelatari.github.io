---
title: "Unable to activate albacore-2.5.13"
layout: post
author: chrispelatari
categories: [rake,albacore]
---

## Unable to activate albacore-2.5.13, because rake-11.1.2 conflicts with rake (~> 10)

I had recently updated Ruby to version 2.3, which updated rake to verison 11 when I did a gem update.

Since I use albacore to build some of my projects, I need this to work. So first, I reverted Ruby back to version 2.1. Then I did a gem uninstall rake and was met with this:

```
$ gem uninstall rake

Select gem to uninstall:
 1. rake-10.4.2
 2. rake-11.1.2
 3. All versions
> 2
Successfully uninstalled rake-11.1.2
```

This was the secret to getting the above error message to clear, and get albacore working again on my windows install.

Hopefully this is fixed in the near future, but until then I thought I would share this workaround.

hth
