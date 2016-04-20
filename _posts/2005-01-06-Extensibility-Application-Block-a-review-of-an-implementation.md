---
layout: post
title: Extensibility Application Block - a review of an implementation.
---
[Royo](http://www.iserializable.com) asks:

<blockquote dir="ltr" style="MARGIN-RIGHT: 0px">
  <p>I'm interested to know whether you found my Extensibility application block 
  useful, or if you had to make many changes to it to make it 
workable.</p></blockquote>

The short answer to this question is: yes and that depends on your 
definition of 'many'.

The <a href="http://weblogs.asp.net/rosherove/archive/2003/11/24/39484.aspx">EAP 
</a>was useful to me: without the ideas and articles supporting it, it would 
have taken me at *least* twice as long to implement a spell checking 
plugin for PostXING. That said, there were some hurdles I had to overcome in 
order to get it working consistently for me.

First, let me say that I wanted to mimic <a href="http://rssbandit.org">RssBandit's</a> plugin architecture because a) 
I have the source code handy and b) it works. RssBandit's method of loading 
plugins (called "ServiceManager")...

<pre><span style="COLOR: gray">/// &lt;summary&gt;
</span><span style="COLOR: gray">/// ServiceManager implements a similar algorithm described in
</span><span style="COLOR: gray">/// <a href="http://msdn.microsoft.com/asp.net/using/building/components/default.aspx?pull=/library/en-us/dnaspp/html/searchforplugins.asp">http://msdn.microsoft.com/asp.net/using/building/components/default.aspx?pull=/library/en-us/dnaspp/html/searchforplugins.asp</a> 
</span><span style="COLOR: gray">/// to find classes in assemblies that implements Syndication.Extensibility.IBlogExtension.
</span><span style="COLOR: gray">/// &lt;/summary&gt;</span></pre>

Well, guess what? The author of the above article and the EAP are one 
and the same! Good news for me.

Okay, that said, I was unable to get the DynamicFindPluginProvider to 
work correctly consistently. The problem was that I was trying to load an 
assembly from within itself (I think - I'm no reflection guru by any means) and 
the result was that when the application was launched standalone it would work, 
when it was launched from the plugin in would b0rk.

I also had to add some properties and methods to the IPlugin 
interface and the AppContext class in order for IPlugin to be even remotely 
useful to me. I found out rather quickly that I was going to need some way to 
configure each IPlugin implementation individually, so I "borrowed" that part of 
the contract from IBlogExtension. A couple of properties were required in my 
case in AppContext - 

<pre>		<span style="COLOR: blue">protected</span> <span style="COLOR: blue">bool</span> _isCallingFromHostApplication = <span style="COLOR: maroon">true</span>;
		<span style="COLOR: blue">public</span> <span style="COLOR: blue">virtual</span> <span style="COLOR: blue">bool</span> IsCallingFromHostApplication{
			<span style="COLOR: blue">get</span>{<span style="COLOR: blue">return</span> _isCallingFromHostApplication;}
			<span style="COLOR: blue">set</span>{_isCallingFromHostApplication = value;}
		}

		<span style="COLOR: blue">protected</span> <span style="COLOR: blue">string</span> _currentEditorText = <span style="COLOR: blue">string</span>.Empty;
		<span style="COLOR: blue">public</span> <span style="COLOR: blue">virtual</span> <span style="COLOR: blue">string</span> CurrentEditorText{
			<span style="COLOR: blue">get</span>{ <span style="COLOR: blue">return</span> _currentEditorText;}
			<span style="COLOR: blue">set</span>{ _currentEditorText = value;}
		}</pre>
    
CurrentEditorText shows up in some of Roy's articles, but not the EAP 
itself. I'm interested in the text, but I can see that CurrentEditorText is not 
generic enough to be included by default. This kind of makes me think that the 
EAP is mis-named: it's really a foundation, or building block, whereas the <a href="http://www.microsoft.com/resources/practices/">Patterns &amp; 
Practices</a> Application Blocks come kind of ready-to-go OOB. That doesn't 
detract from its validity and usefulness - I've just become accustomed to not 
having to modify an "Application Block" to get it working right away. 

*Anyways,* semantics aside, I needed these properties for 
dealing with the IPlugin correctly. The override of CurrentEditorText in my 
app-specific AppContext (called PostXINGAppContext, natch) raises an event 
saying that it was modified on set, and the consuming event loads the text back 
into the editor only if the CurrentEditorText was not set by the calling 
application - I thought that might end up in endless loads of text into the 
editor which would get rid of the usefulness of a plugin. I could be wrong, but 
that's what I went with, okay?:)

I found it useful to inherit my IPlugin implementation from the 
GenericDockablePlugin, even tho there is no UI except for the NetSpell-supplied 
dialogs. This way, I was able to set an icon thru the designer and have it 
embedded as a resource instead of including it with the install of the dll. It 
was just the easiest way to get from idea to implementation for me.

In summary, the EAP is great as a building block for getting plugin 
functionality into your windows forms app. With some minor modifications, I was 
able to pull functionality that was originally going to be part of the host 
application out into a plugin in a few hours.

<p class="media">[ Currently Playing : Tip Your Bartender - Glassjaw - Worship 
&amp; Tribute (2:59) ]</p>