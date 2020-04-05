---
layout: post
title: Using git flow with github for windows
date: 2012-07-02 19:16
author: chrispelatari
comments: true
categories: [Image, professional_geek]
---
I like <a href="http://windows.github.com">github for windows</a>. Seriously, they did a great job with it - kudos, <a href="http://haacked.com">Phil</a>. I like that it has an updateable bash shell ala msysgit. I also like to use <a href="http://github.com/nvie/gitflow">git-flow</a> but alas, this isn’t included with the release. Here is how I got it installed on my system anyway:

First, I cloned the gitflow repository (using github for windows) then opened the shell there. The readme says there is a cmd script in the contrib folder called msysgit-install.cmd so I tried to use this but the script told me it couldn’t find getopt:

<a href="http://chrispelatari.files.wordpress.com/2012/07/get-opt-not-found.png"><img class="alignnone size-full wp-image-1130" alt="get-opt-not-found" src="http://chrispelatari.files.wordpress.com/2012/07/get-opt-not-found.png" width="593" height="88" /></a>

boo.

Fortunately, I have the other install of <a href="http://code.google.com/p/msysgit/">msysgit</a> on my machine so I copied getopt.exe from C:Program FilesGitbin to that fancy path in the image above, along with some supporting dlls

<a href="http://chrispelatari.files.wordpress.com/2012/07/cygwindlls.png"><img class="alignnone size-full wp-image-1131" alt="cygwindlls" src="http://chrispelatari.files.wordpress.com/2012/07/cygwindlls.png" width="109" height="87" /></a>

After doing this, running msysgit-install.cmd copied over the necessary files, and I was able to cd to a repository with only master and develop branches and run git flow init.

<a href="http://chrispelatari.files.wordpress.com/2012/07/git-flow-init.png"><img class="alignnone size-full wp-image-1132" alt="git-flow-init" src="http://chrispelatari.files.wordpress.com/2012/07/git-flow-init.png" width="593" height="343" /></a>

Next step: a feature request to the github for windows team to ask for maybe including at least getopt if not git-flow in the next release?
