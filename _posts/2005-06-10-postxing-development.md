---
layout: post
title: "PostXING development"
description: ""
category: 
tags: []
---
 

<p>I've been working a little on my plugin/provider idea on <a href="http://PostXING.url123.com/main">PostXING</a>. Currently, I have it 
building, but I've had to disable some of the post-build commands because 
although it builds, it doesn't do anything currently and I don't want it to 
overwrite the working copy that I have on my computer.</p>
<p>Interesting aside: I didn't actually <em>remove</em> the commands, but since 
they are all written to a .bat file, you can use normal batch commands - like 
rem - to effectively disable the commands. An example that is currently disabled 
in the branch .csproj file but not in the main trunk:</p>
<p><pre><span style="COLOR: green">rem COPY /Y $(ProjectDir)ReadMe.txt $(TargetDir)ReadMe.txt</span></pre></p>
<p>This way, when I'm ready to actually dogfood my new creation, I just need to 
remove the rem's and I'm good to go.</p>
<p>I've only made progress on the UI so far, but if you want to see the 
progress, the code is always available on <a href="http://vaultpub.sourcegear.com">vaultpub</a>. You can view everything on 
the web <a href="http://vaultpub.sourcegear.com/VaultService/VaultWeb/ShowFolder.aspx?repid=5&amp;path=$/branches/PostXINGv2">over 
here</a>: the login is guest/guest. </p>
<p>As if you cared...</p>
<p>I'm still trying to work out how cross-posting should be implemented. I've 
decided to go with an interface-driven plugin model because I don't have an 
app.config with this app (no reason for that - just haven't needed it yet) and 
I've already got 2 types of interfaces loading as plugins. I have 3(1/2) 
different types of plugin/providers that I want to implement, all of which I 
have access to so I can at least test it a little bit. They will include 
providers using xml-rpc, webservices, and the Atomizer. On the UI side, I'm 
going to do away with as many dialogs as possible. I'm trying to have this app 
have only one or two dialogs where it makes sense. I think everything else 
should just be a "view" on the main form. </p>
<p>I've also imported a couple of controls to the project along with an <a href="http://url123.com/a2nq7">IUI </a>library so different "views" shouldn't be 
too hard to implement I think. Anyways, back to coding...</p>