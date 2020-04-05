---
layout: post
title: How to resolve a binary file conflict with Git
date: 2010-03-05 21:09
author: chrispelatari
comments: true
categories: [professional_geek]
---
<p><a href="http://www.lostechies.com/blogs/joshuaflanagan/archive/2010/01/28/how-to-resolve-a-binary-file-conflict-with-git.aspx">http://www.lostechies.com/blogs/joshuaflanagan/archive/2010/01/28/how-to-resolve-a-binary-file-conflict-with-git.aspx</a></p>
<p>Thank you for that!</p>
<p>Although the message at the end of git status says use git checkout -- 
&lt;file&gt;, that's not it.</p>
<p>"If you prefer to resolve the conflict using their copy, you need to get the 
version of the file from the branch you were trying to merge in:
</p><p /><pre>git checkout otherbranch somefile.dll"</pre>
<p>
</p><p>sweet.</p>
