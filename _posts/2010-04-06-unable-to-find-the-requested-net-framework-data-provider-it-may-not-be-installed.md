---
layout: post
title: Unable to find the requested .Net Framework Data Provider.  It may not be installed.
date: 2010-04-06 11:20
author: chrispelatari
comments: true
categories: [Uncategorized]
---
<pre>    <span style="color:blue;">&lt;</span><span style="color:maroon;">system.data</span><span style="color:blue;">&gt;</span>
        <span style="color:blue;">&lt;</span><span style="color:maroon;">DbProviderFactories</span><span style="color:blue;">&gt;</span>
            <span style="color:blue;">&lt;</span><span style="color:maroon;">remove</span> <span style="color:red;">invariant</span>="<span style="color:blue;">System.Data.SQLite</span>"/<span style="color:blue;">&gt;</span>
            <span style="color:blue;">&lt;</span><span style="color:maroon;">add</span> <span style="color:red;">name</span>="<span style="color:blue;">SQLite Data Provider</span>" <span style="color:red;">invariant</span>="<span style="color:blue;">System.Data.SQLite</span>" <span style="color:red;">description</span>="<span style="color:blue;">.Net Framework Data Provider for SQLite</span>" <span style="color:red;">type</span>="<span style="color:blue;">System.Data.SQLite.SQLiteFactory, System.Data.SQLite</span>"/<span style="color:blue;">&gt;</span>
        <span style="color:blue;">&lt;</span>/<span style="color:maroon;">DbProviderFactories</span><span style="color:blue;">&gt;</span>
    <span style="color:blue;">&lt;</span>/<span style="color:maroon;">system.data</span><span style="color:blue;">&gt;</span></pre>
<p>this happened to me using subsonic on an x64 machine. adding the x64 binary 
to /bin and adding the above to my web.config got me sorted.</p>
