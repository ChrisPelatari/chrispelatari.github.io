---
layout: post
title: Insanely simple GradientPanel for WinForms
date: 2005-08-10 21:01
author: chrispelatari
comments: true
categories: [professional_geek]
---

<p>This has probably been done a hundred times already, but I couldn't find one 
in the first few pages of google results, so I wrote my own in ~40 lines of 
C#:</p><pre><span style="color:blue;">using</span> System;<br /><span style="color:blue;">using</span> System.ComponentModel;<br /><span style="color:blue;">using</span> System.Drawing;<br /><span style="color:blue;">using</span> System.Drawing.Drawing2D;<br /><span style="color:blue;">using</span> System.Windows.Forms;<br /><br /><span style="color:blue;">namespace</span> PostXING.Controls<br />{<br />	<span style="color:gray;">/// &lt;summary&gt;<br /></span>	<span style="color:gray;">/// GradientPanel is just like a regular panel except it optionally  <br /></span>	<span style="color:gray;">/// shows a gradient.<br /></span>	<span style="color:gray;">/// &lt;/summary&gt;<br /></span>	[ToolboxBitmap(<span style="color:blue;">typeof</span>(Panel))]<br />	<span style="color:blue;">public</span> <span style="color:blue;">class</span> GradientPanel : Panel<br />	{<br />		<span style="color:gray;">/// &lt;summary&gt;<br /></span>		<span style="color:gray;">/// Property GradientColor (Color)<br /></span>		<span style="color:gray;">/// &lt;/summary&gt;<br /></span>		<span style="color:blue;">private</span> Color _gradientColor;<br />		<span style="color:blue;">public</span> Color GradientColor {<br />			<span style="color:blue;">get</span> { <span style="color:blue;">return</span> <span style="color:blue;">this</span>._gradientColor;}<br />			<span style="color:blue;">set</span> { <span style="color:blue;">this</span>._gradientColor = value;}<br />		}<br /><br />		<span style="color:gray;">/// &lt;summary&gt;<br /></span>		<span style="color:gray;">/// Property Rotation (float)<br /></span>		<span style="color:gray;">/// &lt;/summary&gt;<br /></span>		<span style="color:blue;">private</span> <span style="color:blue;">float</span> _rotation;<br />		<span style="color:blue;">public</span> <span style="color:blue;">float</span> Rotation {<br />			<span style="color:blue;">get</span> { <span style="color:blue;">return</span> <span style="color:blue;">this</span>._rotation;}<br />			<span style="color:blue;">set</span> { <span style="color:blue;">this</span>._rotation = value;}<br />		}<br /><br />		<span style="color:blue;">protected</span> <span style="color:blue;">override</span> <span style="color:blue;">void</span> OnPaint(PaintEventArgs e) {<br />                        <font color="blue">if<font color="black">(e.ClipRectangle.IsEmpty)</font> return</font><font color="black">; <font color="green">//why draw if non-visible?</font><br /> </font><br /><br />			<span style="color:blue;">using</span>(LinearGradientBrush lgb = <span style="color:blue;">new</span> <br />                           LinearGradientBrush(<span style="color:blue;">this</span>.ClientRectangle, <br />		              <span style="color:blue;">this</span>.BackColor, <br />		              <span style="color:blue;">this</span>.GradientColor, <br />		              <span style="color:blue;">this</span>.Rotation)){<br />				e.Graphics.FillRectangle(lgb, <span style="color:blue;">this</span>.ClientRectangle);<br />			}<br /><br /><font color="#0000ff">                        base</font>.OnPaint (e); <font color="green">//right, want anything handled to be drawn too.</font>

		}
	}
}</pre>
<p>There it is. Enjoy!</p>
<p class="media">[ Currently Playing :  New Way Home - Foo Fighters - The 
Colour And The Shape (5:42) ]</p>
