---
layout: post
title: "Embrace and Extend: MikeDub's IUI article"
---
I've been doing a lot of that lately (embracing and 
extending). So I'm reading thru <a href="http://www.mikedub.net/windowsformsredux/">Mike</a>'s <a href="http://url123.com/a2nq7">latest article</a>, thinking how can I apply this 
to an application I'm currently developing?

In the article, he mentions that Office 2003 uses both a deductive and 
inductive UI for various parts of the interface (see his article for a much 
better explanation than I could give you.) So I tried it out. I downloaded the 
code and applied something very similar to the Office example shown in the 
article using <a href="http://divil.co.uk/net/">Tim Dawson's </a>awesome <a href="http://divil.co.uk/net/controls/sandbar/">Sandbar </a> library.

There was a problem, though. By virtue of a vertical scrollbar, enabled, 
disabled, visible, or invisible, it always showed up in a space where I need 
those 23 pixels. It's important. I wanted to take the code that was in the 
example download and make sure I could remove the scrollbar without breaking 
things. Well, the way that the code is set up now, you've got to have a Frame 
class to associate with each Page class. Period. 

At first I tried subclassing the Frame class, but the VS.NET designer did not 
like that too much. We want to play nice with the designer always, right? Sure 
we do. (If you don't think so about asp.net, you will soon I'm sure:) What was 
missing from this puzzle? Looking at the Frame class a little bit further, it 
became obvious: this code is begging for an interface implementation. Just 
taking the public methods that were exposed in the Frame class, I came up with 
the IFrame interface:

<pre><font color="#0000ff">public</font> <font color="#0000ff">interface</font> IFrame	{
	
	<font color="#0000ff">void</font> Go(Page page);

	<font color="#0000ff">void</font> Go(Type pageType);

	<font color="#0000ff">void</font> GoBack();

	<font color="#0000ff">void</font> GoBack(<font color="#0000ff">int</font> n);

	<font color="#0000ff">void</font> GoForward();

	<font color="#0000ff">void</font> GoForward(<font color="#0000ff">int</font> n);

	<font color="#0000ff">void</font> GoHome();

	<font color="#0000ff">void</font> PageDown();

	<font color="#0000ff">void</font> PageEnd();

	<font color="#0000ff">void</font> PageHome();

	<font color="#0000ff">void</font> PageUp();
}</pre>

Then I changed the Page class's reference to its parent frame to hold an 
IFrame reference:

<pre><font color="#0000ff">public</font> IFrame Frame{
		get{ <font color="#0000ff">return</font> frame;}<font color="#008200">//of course, the private reference is also IFrame
</font>		set{ frame = value;}
}</pre>

Bam. That's it. I then created a class that I called StaticFrame and removed 
the horizontal and vertical scrollbars from it, implementing only those methods 
defined in the interface and those required to maintain NavigationContext. Now 
I've got a great navigation story for a sidebar/taskpane type interface in my 
applications.