---
layout: post
title: How not to use the PictureBox control.
date: 2005-10-19 21:04
author: chrispelatari
comments: true
categories: [professional_geek]
---

<p>I was having this problem in an application that I've been working on where I 
was drawing data points onto a PictureBox control - kind of like a canvas. The 
problem only showed up when a lot of data was thrown at the PictureBox: instead 
of seeing my data, I would see a loverly <strong><font color="red" size="6">big red 
x</font></strong>.</p>
<p>So I did some chasing down a few rabbit holes (apparently this is a difficult 
issue to pinpoint - I found loads of unanswered forum/newsgroup posts about a 
red x) and found <a href="http://www.bobpowell.net/faqmain.htm">Bob 
Powell's GDI+ faq</a>. Specifically, I found a good overview of <a href="http://www.bobpowell.net/pictureboxhowto.htm">How not to use the 
PictureBox control.</a> After a few trials of throwing largish datasets at 
my picturebox canvas (that had yeilded those nasty red x's after a few screen 
refreshes just minutes before) it seems like the advice in that article just may 
have solved the problem.</p>
<p>We had been drawing to a Graphics object, then using that to spit out an 
image to the PictureBox's .Image property:</p><pre>Graphics g = pbxCanvas.CreateGraphics();

<span style="color:green;">//draw to graphics
</span>
pbxCanvas.Image = GetCanvasImage();</pre>
<p>instead, now we create the Graphics object off of the .Image in the first 
place. It takes a little bit more setup, but I have yet to run into the red x 
again since implementing this code:</p><pre><span style="color:blue;">if</span>(pbxCanvas.Image == <span style="color:blue;">null</span>){
	pbxCanvas.Image = <span style="color:blue;">new</span> Bitmap(pbxCanvas.Width, pbxCanvas.Height);
}

Graphics g = Graphics.FromImage(pbxCanvas.Image);

<span style="color:green;">//draw to graphics
</span>
pbxCanvas.Image = GetCanvasImage();
pbxCanvas.Invalidate();</pre>
<p>Who would have thought that a call to Control.CreateGraphics would be so 
harmful?</p>
