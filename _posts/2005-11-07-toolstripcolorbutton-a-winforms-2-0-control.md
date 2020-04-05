---
layout: post
title: ToolStripColorButton&#58; a WinForms 2.0 Control
date: 2005-11-07 18:27
author: chrispelatari
comments: true
categories: [professional_geek]
---
Disclaimer: the code for showing the color menu is totally ripped off of a <a href="http://codeproject.com/cs/miscctrl/ColorButton.asp">CodeProject
article</a>. I just took the ColorPanel part and parented it with a
ToolStripButton. The idea works, tho.

<a href="http://chrispelatari.files.wordpress.com/2005/11/toolstripcolorbuttonxp_clos.jpg"><img class="alignnone size-full wp-image-1174" alt="ToolStripColorButtonXP_clos" src="http://chrispelatari.files.wordpress.com/2005/11/toolstripcolorbuttonxp_clos.jpg" width="179" height="185" /></a>

Here's the source: <a href="http://vaultpub.sourcegear.com/VaultService/VaultWeb/GetFile.aspx?repid=5&amp;path=%24%2ftrunk%2fv2.0%2fPostXING.Controls%2fToolStripColorButton.cs&amp;version=2">ToolStripColorButton.cs</a> (login
is guest/guest).

I've been working recently to bring PostXING v2 to .net v2. Part of this
process has shown me that Divelements' SandBar menu system (the last freeware
version) doesn't like to be in a nested UserControl after a recompile. Throws
all kinds of errors that are obfuscated and painted directly on the control in
the designer. Unfortunately, I can't try a newer version of SandBar because they
discontinued the freeware versions that they used to have. Shame, it's a really
good library.

So anyways, I find myself needing a similar experience to the ColorMenu that
I extended that comes as an example with the trial download. Now that we have a
first-class menu system in System.Windows.Forms, I decided to see if I could
create something that kept the simplicity of the ColorMenu. The
ToolStripColorButton simply has a subclass called ColorPanel that inherits Form.
When you click on the button, the form is shown. When a user selects a color, a
changed event is thrown and you can do what you want with the resulting color by
handling this event:
<pre><span style="color:blue;">private</span> <span style="color:blue;">void</span> btnFontColor_Changed(<span style="color:blue;">object</span> sender, EventArgs e)
{
	<span style="color:blue;">this</span>.DesignEditor.TextFormatting.ForeColor = <span style="color:blue;">this</span>.btnFontColor.Color;
}</pre>
A couple of points that could be extended: The gradient background looks
all wrong with the default XP themes. I wonder if there's a way to query what
the start/finish colors are for the current theme w/o going into unmanaged code?
Heck, even <strong>with</strong> unmanaged code (via P/Invoke) would be fine.
This same problem shows up for the GradientPanel I
recently posted. Something to look into, anyways. There's also the
extension point of adding the actual color as the image instead of using a stock
icon or something similar. The code to do it is basically in the CodeProject
article linked above, I was just happy with the icons for my current purposes.

[ Currently Playing : Drive Slow (Feat. Paul Wall &amp; - Kanye West - Late
Registration (4:32) ]
