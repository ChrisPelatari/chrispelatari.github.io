---
title: "Liquid Exception: no implicit conversion of Array into String in _layouts"
layout: post
author: chrispelatari
categories: [jekyll,liquid,github-pages]
---
"Liquid Exception: no implicit conversion of Array into String in /\_layouts/post.html"

I was attempting to finally add an archive page to my jekyll site here on github-pages...I got the page in place and updated all of the dependencies, including a new Ruby environment to match what's on github's servers.

After I updated, I started getting the above error. It's hard to search for. At the time that I did, there was only 1 semi-relevant post I could find. The above error didn't make a lot of sense to me because I (obviously) don't dig into this every day. It does however give a couple of clues...there is a post that is handing what looks like an Array to a variable that expects a string. And it was a post from 2010. Only one, out of the 400+ posts that are currently here. It was in my title which had to be changed from this:

```
title: [[deactivatedstyle]]
```

to this:

```
title: '\[deactivatedstyle\]'
```

Because I have changed content storage systems so many times over the years, this became a problem (along with images...gotta be real careful where those go) of front matter/ruby not treating everything after title: as an actual string, which is not a problem for the sql sproc parameters that used to hold that field.
