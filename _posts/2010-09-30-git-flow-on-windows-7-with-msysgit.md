---
layout: post
title: GIT flow on windows 7 with msysgit
date: 2010-09-30 15:07
author: chrispelatari
comments: true
categories: [professional_geek]
---
<p>this is <a href="http://http://github.com/nvie/gitflow/issues/issue/25">outlined on github</a> by psampaio:</p>  <blockquote>   <p>I managed to get git flow working with msysGit, but needed some hacks on my setup. First, I copied all the git* files to libexecgit-core. Then replaced shFlags like snaewe mentioned, but &lt;install_dir&gt; for me was also libexecgit-core.</p>    <p>Git flow complained about getopt. I got it from cygwin (package utils_linux*) and copied the getopt.exe to the bin folder. Also had to copy 4 more files from cygwin to the bin folder (cyggcc_s-1.dll, cygiconv-2.dll, cygintl-8.dll and cygwin1.dll).</p>    <p>Like I said in the beginning, this is a hacky solution but it did work for me.</p> </blockquote>  <p>I simply followed what they said and have gotten this working on a few windows 7 machines. I even took it a step further and created a couple of zip files of the dlls and scripts required: <a href="http://dl.dropbox.com/u/88271/bin.zip">bin.zip</a> and <a href="http://dl.dropbox.com/u/88271/git-core.zip">git-core.zip</a></p>  <p>To install these for mSysGit:</p>  <ol>   <li>copy bin.zip to C:Program FilesGit </li>    <li>unzip bin.zip </li>    <li>copy git-core.zip to C:Program FilesGitlibexec </li>    <li>unzip git-core.zip </li> </ol>  <p> </p>  <p>[it’s important that they are unzipped from the correct place, but you knew that :)]</p>  <p>and that’s all there is to it. you should now be able to go to a git repository on windows with mSysGit, type git flow init, and be presented with the git flow setup prompts.</p>  <p>enjoy!</p>
