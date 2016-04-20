---
layout: post
title: Getting a temporary filename the easy way
date: 2006-05-04 15:02
author: chrispelatari
comments: true
categories: [Uncategorized]
---

<p>If you need to generate temporary / semi-unique filenames, here is a little 
snippet that uses the framework:</p><pre><span style="color:blue;">using</span> System.IO;

<span style="color:blue;">string</span> GetTempFileName(){
	<span style="color:blue;">return</span> Path.GetFileNameWithoutExtension(Path.GetTempFileName());
}</pre>
<p>As the name implies, this will return the temporary name of a file without 
the extension, so it's up to you to add whatever filetype you may be trying to 
create. For example, let's say I wanted to generate a .gif:</p><pre><span style="color:blue;">string</span> GetTempGifFileName(){
	<span style="color:blue;">return</span> <span style="color:blue;">string</span>.Format(<span style="color:maroon;">"{0}.{1}"</span>, GetTempFileName(), <span style="color:maroon;">"gif"</span>);
}</pre>
<p>I had overlooked this little piece of functionality because the component 
that I was using generated filenames with GUIDs, so I never really worried about 
it. Way to make my life easier, .netfx :)</p>
<p class="media">[ Currently Playing : Mississippi Queen - Ozzy Osbourne - Under 
Cover (4:11) ]</p>
