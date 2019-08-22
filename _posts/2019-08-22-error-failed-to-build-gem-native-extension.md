---
title: "ERROR: Failed to build gem native extension"
layout: post
author: chrispelatari
categories: [Ruby, Linux, Unbuntu]
---

I ran into this problem on a fresh install of Ubuntu 18.04.3 LTS. I had not installed development tools yet, so I found [this](https://github.com/travis-ci/travis.rb/issues/558#issuecomment-355962361) which prompted me to add:

- ruby-dev
- gcc
- libffi-dev
- make

That got the gems building, but it kept giving me an error after build:
```
checking for gzdopen() in -lz... no
zlib is missing; necessary for building libxml2
```

well shit. 

```
 sudo apt install zlib
Reading package lists... Done
Building dependency tree       
Reading state information... Done
E: Unable to locate package zlib
```

According to [this](https://askubuntu.com/questions/508934/how-to-install-libpng-and-zlib) I then ran:
```
sudo apt-get install zlib1g-dev
```

And boom.