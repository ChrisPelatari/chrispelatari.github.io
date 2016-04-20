---
layout: post
title: "ReverseDOS in Community Server"
description: ""
category: 
tags: []
---
 

<p>After another slew of referrer/comment spam that showed up in my blog this 
morning, I went ahead and downloaded Mike's <a href="http://angrypets.com/tools/rdos/">ReverseDOS</a>.</p>
<p>I followed the steps outlined for setup, but it didn't quite work the way it 
was outlined at first - I got the dreaded "yellow screen of death". This was due 
to the entries that I had made in the web.config. So I looked at the entries 
that were already in there, and I noticed that some <span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">section/</span><span style="COLOR: blue">&gt;</span> nodes were added to the <span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">system.web/</span><span style="COLOR: blue">&gt;</span> node. Moving the default configuration from 
looking like this:</p>

<p><pre><span style="COLOR: blue">&lt;</span>!-- copy and paste the following code --<span style="COLOR: blue">&gt;</span>
<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">configSections</span><span style="COLOR: blue">&gt;</span>
   <span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">sectionGroup</span> <span style="COLOR: red">name</span>="<span style="COLOR: dodgerblue">AngryPets</span>" <span style="COLOR: blue">&gt;</span>
      <span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">section</span> <span style="COLOR: red">name</span>="<span style="COLOR: dodgerblue">ReverseDOS</span>" <span style="COLOR: red">type</span>="<span style="COLOR: dodgerblue">AngryPets.Web.Frameworks.ReverseDOS.FilterConfigHandler, AngryPets.Web.Frameworks.ReverseDOS</span>" /<span style="COLOR: blue">&gt;</span>
   <span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">sectionGroup</span><span style="COLOR: blue">&gt;</span>
<span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">configSections</span><span style="COLOR: blue">&gt;</span></pre>
<p class="media">Instead, mine now looks like this:</p><pre><span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">sectionGroup</span> <span style="COLOR: red">name</span>="<span style="COLOR: dodgerblue">system.web</span>"<span style="COLOR: blue">&gt;</span>
	<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">section</span> <span style="COLOR: red">name</span>="<span style="COLOR: dodgerblue">membership</span>" <span style="COLOR: red">type</span>="<span style="COLOR: dodgerblue">Microsoft.ScalableHosting.Configuration.MembershipConfigHandler, MemberRole, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b7c773fb104e7562</span>"/<span style="COLOR: blue">&gt;</span>
	<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">section</span> <span style="COLOR: red">name</span>="<span style="COLOR: dodgerblue">roleManager</span>" <span style="COLOR: red">type</span>="<span style="COLOR: dodgerblue">Microsoft.ScalableHosting.Configuration.RolesConfigHandler, MemberRole, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b7c773fb104e7562</span>"/<span style="COLOR: blue">&gt;</span>
	<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">section</span> <span style="COLOR: red">name</span>="<span style="COLOR: dodgerblue">profile</span>" <span style="COLOR: red">type</span>="<span style="COLOR: dodgerblue">Microsoft.ScalableHosting.Configuration.ProfileConfigHandler, MemberRole, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b7c773fb104e7562</span>"/<span style="COLOR: blue">&gt;</span>
	<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">section</span> <span style="COLOR: red">name</span>="<span style="COLOR: dodgerblue">anonymousIdentification</span>" <span style="COLOR: red">type</span>="<span style="COLOR: dodgerblue">Microsoft.ScalableHosting.Configuration.AnonymousIdConfigHandler, MemberRole, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b7c773fb104e7562</span>"/<span style="COLOR: blue">&gt;</span>
	<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">section</span> <span style="COLOR: red">name</span>="<span style="COLOR: dodgerblue">ReverseDOS</span>" <span style="COLOR: red">type</span>="<span style="COLOR: dodgerblue">AngryPets.Web.Frameworks.ReverseDOS.FilterConfigHandler, AngryPets.Web.Frameworks.ReverseDOS</span>" /<span style="COLOR: blue">&gt;</span>
<span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">sectionGroup</span><span style="COLOR: blue">&gt;</span></pre></p>
<p class="media">And I of course moved the ReverseDOS node to be under system.web. 
We'll see how this pans out, but I thought I would put it out there just in case 
someone else was having issues with it.</p>
<p class="media">[ Currently Playing : Stinkfist - Tool - Aenima (5:10) 
]</p>