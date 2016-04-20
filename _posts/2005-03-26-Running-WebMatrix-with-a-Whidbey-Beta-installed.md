---
layout: post
title: Running WebMatrix with a Whidbey Beta installed
---
I took a chance and installed a CTP of Whidbey on my laptop. Thing is, I 
still use WebMatrix from time to time for POC stuff for v1.x of asp.net.

Problem is, when you run the Cassini webserver from webmatrix, it picks up 
the latest version of the .netfx and will give you different errors based on 
which version is installed. To get around this and ensure that the WebServer.exe 
runs on version 1.1 of the .netfx, simply add a WebServer.exe.config file with 
the following contents:

<pre><span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">configuration</span><span style="COLOR: blue">&gt;</span>
	<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">startup</span><span style="COLOR: blue">&gt;</span>
		<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">requiredRuntime</span> <span style="COLOR: red">version</span>="<span style="COLOR: blue">v1.1.4322</span>"/<span style="COLOR: blue">&gt;</span>
	<span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">startup</span><span style="COLOR: blue">&gt;</span>
<span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">configuration</span><span style="COLOR: blue">&gt;</span></pre>

If you want to ensure WebMatrix runs on version 1.1 of the .netfx, you can 
add the above startup element to WebMatrix.exe.config.