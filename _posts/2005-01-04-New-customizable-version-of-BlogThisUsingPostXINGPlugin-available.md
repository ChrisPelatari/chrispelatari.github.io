---
layout: post
title: New customizable version of BlogThisUsingPostXINGPlugin available
---
This <a href="http://PostXING.url123.com/plugin1.0.5004.1">new version of the 
BlogThisUsingPostXINGPlugin</a> handles customizing the transform used to output 
into a new Post in <a href="http://PostXING.url123.com/main">PostXING</a>. For 
example, say I want to have the title of the post referenced in the post body. I 
would start off with the LinkOnly.xslt option:

<pre><span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  1</span> <span style="COLOR: blue">&lt;?</span><span style="COLOR: maroon">xml</span> <span style="COLOR: red">version</span>="<span style="COLOR: dodgerblue">1.0</span>" <span style="COLOR: blue">?&gt;</span>
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  2</span> <span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">xsl:stylesheet</span> <span style="COLOR: red">version</span>="<span style="COLOR: dodgerblue">1.0</span>" <span style="COLOR: red">xmlns:xsl</span>="<span style="COLOR: dodgerblue">http://www.w3.org/1999/XSL/Transform</span>"<span style="COLOR: blue">&gt;</span>
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  3</span> 	<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">xsl:output</span> <span style="COLOR: red">method</span>="<span style="COLOR: dodgerblue">html</span>" /<span style="COLOR: blue">&gt;</span> 
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  4</span> 	<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">xsl:variable</span> <span style="COLOR: red">name</span>="<span style="COLOR: dodgerblue">feed-title</span>" <span style="COLOR: red">select</span>="<span style="COLOR: dodgerblue">/rss/channel/title</span>" /<span style="COLOR: blue">&gt;</span>
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  5</span> 	
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  6</span> 	<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">xsl:template</span> <span style="COLOR: red">match</span>="<span style="COLOR: dodgerblue">/</span>"<span style="COLOR: blue">&gt;</span>
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  7</span> 		<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">xsl:apply-templates</span> <span style="COLOR: red">select</span>="<span style="COLOR: dodgerblue">//item</span>" /<span style="COLOR: blue">&gt;</span>
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  8</span> 	<span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">xsl:template</span><span style="COLOR: blue">&gt;</span>
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  9</span> 
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 10</span> 	<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">xsl:template</span> <span style="COLOR: red">match</span>="<span style="COLOR: dodgerblue">/rss/channel/item</span>"<span style="COLOR: blue">&gt;</span>
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 11</span> 		<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">html</span><span style="COLOR: blue">&gt;</span>
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 12</span> 		<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">title</span><span style="COLOR: blue">&gt;</span>RE: <span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">xsl:value-of</span> <span style="COLOR: red">select</span>="<span style="COLOR: dodgerblue">title</span>" /<span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">title</span><span style="COLOR: blue">&gt;</span>
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 13</span> 		<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">xsl:choose</span><span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">xsl:when</span> <span style="COLOR: red">test</span>="<span style="COLOR: dodgerblue">link</span>"<span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span>a <span style="COLOR: red">href</span>="<span style="COLOR: dodgerblue">{link}</span>"<span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">xsl:value-of</span> <span style="COLOR: red">select</span>="<span style="COLOR: dodgerblue">$feed-title</span>" /<span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">a</span><span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">xsl:when</span><span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">xsl:otherwise</span><span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">xsl:value-of</span> <span style="COLOR: red">select</span>="<span style="COLOR: dodgerblue">$feed-title</span>" /<span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">xsl:otherwise</span><span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">xsl:choose</span><span style="COLOR: blue">&gt;</span>
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 14</span> 		<span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">html</span><span style="COLOR: blue">&gt;</span>
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 15</span> 	<span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">xsl:template</span><span style="COLOR: blue">&gt;</span>
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 16</span> <span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">xsl:stylesheet</span><span style="COLOR: blue">&gt;</span></pre>

Line 13 is the key line. All I did was change the use of 
xsl:variable to the actual title that is context-specific in this case. So we 
now have:

<pre><span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  1</span> <span style="COLOR: blue">&lt;?</span><span style="COLOR: maroon">xml</span> <span style="COLOR: red">version</span>="<span style="COLOR: dodgerblue">1.0</span>" <span style="COLOR: blue">?&gt;</span>
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  2</span> <span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">xsl:stylesheet</span> <span style="COLOR: red">version</span>="<span style="COLOR: dodgerblue">1.0</span>" <span style="COLOR: red">xmlns:xsl</span>="<span style="COLOR: dodgerblue">http://www.w3.org/1999/XSL/Transform</span>"<span style="COLOR: blue">&gt;</span>
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  3</span> 	<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">xsl:output</span> <span style="COLOR: red">method</span>="<span style="COLOR: dodgerblue">html</span>" /<span style="COLOR: blue">&gt;</span> 
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  4</span> 	<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">xsl:variable</span> <span style="COLOR: red">name</span>="<span style="COLOR: dodgerblue">feed-title</span>" <span style="COLOR: red">select</span>="<span style="COLOR: dodgerblue">/rss/channel/title</span>" /<span style="COLOR: blue">&gt;</span>
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  5</span> 	
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  6</span> 	<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">xsl:template</span> <span style="COLOR: red">match</span>="<span style="COLOR: dodgerblue">/</span>"<span style="COLOR: blue">&gt;</span>
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  7</span> 		<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">xsl:apply-templates</span> <span style="COLOR: red">select</span>="<span style="COLOR: dodgerblue">//item</span>" /<span style="COLOR: blue">&gt;</span>
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  8</span> 	<span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">xsl:template</span><span style="COLOR: blue">&gt;</span>
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  9</span> 
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 10</span> 	<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">xsl:template</span> <span style="COLOR: red">match</span>="<span style="COLOR: dodgerblue">/rss/channel/item</span>"<span style="COLOR: blue">&gt;</span>
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 11</span> 		<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">html</span><span style="COLOR: blue">&gt;</span>
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 12</span> 		<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">title</span><span style="COLOR: blue">&gt;</span>RE: <span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">xsl:value-of</span> <span style="COLOR: red">select</span>="<span style="COLOR: dodgerblue">title</span>" /<span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">title</span><span style="COLOR: blue">&gt;</span>
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 13</span> 		<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">xsl:choose</span><span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">xsl:when</span> <span style="COLOR: red">test</span>="<span style="COLOR: dodgerblue">link</span>"<span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span>a <span style="COLOR: red">href</span>="<span style="COLOR: dodgerblue">{link}</span>"<span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">xsl:value-of</span> <span style="COLOR: red">select</span>="<span style="COLOR: dodgerblue">title</span>" /<span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">a</span><span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">xsl:when</span><span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">xsl:otherwise</span><span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">xsl:value-of</span> <span style="COLOR: red">select</span>="<span style="COLOR: dodgerblue">title</span>" /<span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">xsl:otherwise</span><span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">xsl:choose</span><span style="COLOR: blue">&gt;</span>
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 14</span> 		<span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">html</span><span style="COLOR: blue">&gt;</span>
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 15</span> 	<span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">xsl:template</span><span style="COLOR: blue">&gt;</span>
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 16</span> <span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">xsl:stylesheet</span><span style="COLOR: blue">&gt;</span></pre>

Subtle difference, but it changes a post from this:

<a href="http://weblogs.asp.net/fbouma/archive/2005/01/03/345841.aspx">Frans 
Bouma's blog</a> 

to this:

<a href="http://weblogs.asp.net/fbouma/archive/2005/01/03/345841.aspx">Template 
Studio for LLBLGen Pro released!</a> 

I only left the three default options for formatting in there 
with the idea that most of the time, I would only want to use one of these 
anyways. This opens up the door for this plugin to be completely customized, to 
where the descriptions don't mean anything for the content of the actual 
transform.

<p class="media">[ Currently Playing : Killer Is Me - Alice in Chains - Unplugged 
(5:23) ]</p>