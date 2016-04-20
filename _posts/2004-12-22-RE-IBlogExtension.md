---
layout: post
title: "RE: IBlogExtension"	
---
<blockquote xmlns:xhtml="http://www.w3.org/1999/xhtml">
  <p xmlns="http://www.w3.org/1999/xhtml"><a href="http://yexley.net/blogs/bob/archive/2004/11/30/958.aspx">Bob wants to 
  see some integration of RssBandit and PostXING.</a> </p>
  <p xmlns="http://www.w3.org/1999/xhtml">This was an idea I had really early on 
  simply because a lot of the features in <a href="http://PostXING.url123.com/main">PostXING</a> were, <em>ahem, 
  </em>borrowed from w.bloggar, and RssBandit already supports a plugin that 
  starts w.bloggar for posting to a weblog. So, why couldn't I do something 
  similar? </p>
  <p xmlns="http://www.w3.org/1999/xhtml">Well, I thought that it had something 
  to do with implementing IBlogExtension, for which I couldn't find too much 
  documentation. Maybe it's such a simple thing to implement that only a 
  yutz like me would need documentation. I honestly don't know and haven't 
  looked into it too much simply because I didn't have an immediate need for it. 
  </p>
  <p xmlns="http://www.w3.org/1999/xhtml">Once Dare adds deleting capabilities 
  to <a href="http://rssbandit.org/">RssBandit</a>, I have a feeling that it's 
  going to become my default aggregator again. After that, look out for an 
  RssBandit plugin to post using PostXING.</p>
  <p class="media" xmlns="http://www.w3.org/1999/xhtml">[ Currently Playing : Love 
  Life - Fatboy Slim - Halfway Between the Gutter and Stars(6:58) 
  ]</p></blockquote>
  
  <i>[Via <a href="http://www.chrisfrazier.net/blog/posts/638.aspx">Blue 
Phoenix</a>]</i> 

I got a rudimentary version of this working. I couldn't figure out how to 
download the original post into RssBandit, so I'm just using my original reply 
to the post.

I'd like to thank <a href="http://haacked.com/">Haacked</a> for 
providing a <a href="http://haacked.com/archive/2004/06/19/651.aspx">series 
</a>of <a href="http://www.rssbandit.org/docs/html/advanced/building_and_using_bandit_plugins.htm">walkthrus 
</a>as well as a <a href="http://haacked.com/archive/2004/12/04/1697.aspx">code 
download </a>for an improved version of "Blog This with w.bloggar..." which I 
basically hacked to work with PostXING. I'll probably release this closer to the 
new year or after the first so I can make sure that everything is working okay 
- the only version that is working correctly for me so far is the full 
version. A new version of PostXING will be necessary to make this work as well - 
I never thought to make sure that any application that knew or cared could find 
out where PostXING lived...so I made this happen with a simple text file and a 
call to 

<pre>System.Reflection.Assembly.GetEntryAssembly().Location;</pre>

Also, I found the need to close off the StreamWriter that was 
being used to write the temp file using XslTransform b/c I was getting access is 
denied errors, so the code that did that now looks like so:

<pre>	XslTransform transform = <span style="COLOR: blue">new</span> XslTransform();
	transform.Load(<span style="COLOR: blue">new</span> XmlTextReader(XsltStream), <span style="COLOR: blue">null</span>, <span style="COLOR: blue">null</span>);


	<span style="COLOR: blue">string</span> tempfile = Path.GetTempFileName();<span style="COLOR: green">//@"c:\tmp\plugin\" + this.BlogType.ToString() + ".html";  
</span>	StreamWriter sw = <span style="COLOR: blue">new</span> StreamWriter(tempfile);
	transform.Transform(rssFragment, <span style="COLOR: blue">null</span>, sw, <span style="COLOR: blue">null</span>);

	sw.Close();</pre>
  
So with that and a little bit of <a href="http://blogs.msdn.com/smourier/archive/2003/06/04/8265.aspx">Agility</a>, 
this was about a two-hour enhancement. Next I'm going to look into creating 
(well, probably "borrowing") a plugin architecture so that I can create a spell 
checking plugin for <a href="http://PostXING.url123.com/main">PostXING</a> without bloating the 
main download too much.

<p class="media">[ Currently Playing : Burn Away - Foo Fighters - One by One 
(4:57) ]</p>