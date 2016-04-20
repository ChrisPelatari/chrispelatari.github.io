---
layout: post
title: "switched engines again"
description: "extended babbling about changing blog enginges for maybe the dozenth time."
category: as-if-you-cared
tags: [blog]
---

this time from WordPress to jekyll. I had already toyed with getting some content over into jekyll along with a few extra tools in Jekyll-bootstrap. WordPress was winning the blog wars at the time and the import from my previous engine (dotText) seemed more complete over there.

But jekyll plays to my geek tendencies. Markdown makes authoring posts fairly easy and eliminates the need for a blog posting tool - which is how I spent a lot of my spare time about a decade ago.

I imported the WordPress content using a tool called [wpXml2Jekyll](https://github.com/theaob/wpXml2Jekyll). It was very straightforward, I like that. Bonus: despite being a "windows" application, it works on OS X using Mono. Simply add mono to the beginning of the command:

```$
mono wpXml2Jekyll.exe [wordpress export file] [output directory]
```

I think I still have to go thru some posts for some broken images, transfer some over etc. fairly simple transition tho.
