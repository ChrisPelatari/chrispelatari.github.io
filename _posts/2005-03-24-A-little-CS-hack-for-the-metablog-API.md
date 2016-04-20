---
layout: post
title: A little CS hack for the metablog API
---
[Keith](http://sol3.net/blogs/starpilot/) told me that 
CSBlogs was returning relative urls for its Metablog API implementation. After I 
installed it, I noticed the same thing - so I decided to hack it a little bit 
and find out what was going wrong. It turns out that the software is just doing 
what the guys at telligent are telling it to - thankfully I've got the code and 
I can poke around when I find little issues like this :)

First, I added a call to the Globals class to return a formatted url with the 
application path intact. This was in Components.SiteUrlsData.cs:

<pre><span style="COLOR: blue">public</span> <span style="COLOR: blue">virtual</span> <span style="COLOR: blue">string</span> FormatUrl(<span style="COLOR: blue">string</span> name, <span style="COLOR: blue">params</span> <span style="COLOR: blue">object</span>[] parameters)
{      	

    <span style="COLOR: blue">if</span>(parameters == <span style="COLOR: blue">null</span>)
        <span style="COLOR: blue">return</span> Globals.FullPath(<span style="COLOR: blue">this</span>.Paths[name]);

    <span style="COLOR: blue">else</span>
        <span style="COLOR: blue">return</span> Globals.FullPath(<span style="COLOR: blue">string</span>.Format(Paths[name],parameters));
}</pre>

But wait! This causes the rss feed to show up with something silly like http: 
/ /localhost/cshttp://localhost/cs/blog... for the links in the RSS and Atom 
feeds produced by CSBlogs. So, I tried it without the "HostPath" to see if I 
could get the same results. This was in 
Blogs.Components.BaseWeblogSyndicationHandler:

<pre><span style="COLOR: gray">/// <summary>
</summary></span><span style="COLOR: gray">/// Appends http://Host:Port to all blog urls
</span><span style="COLOR: gray">/// 
</span><span style="COLOR: blue">protected</span> <span style="COLOR: blue">override</span> <span style="COLOR: blue">string</span> BaseUrl
{
    <span style="COLOR: blue">get</span>
    {
        <span style="COLOR: blue">return</span> <span style="COLOR: maroon">""</span>; <span style="COLOR: green">//return Globals.HostPath(Context.Request.Url);
</span>    }
}</pre>

That's it right? Nope, not if you have galleries enabled. One of the methods 
(that I know of :) uses the modified FormatUrl above to try and get a MapPath to 
a directory. You'll find out really quickly that MapPath doesn't like 
fully-qualified urls passed to it...I know I did. So, I modified one more line 
to make sure that I've got a relative path passed into the photo gallery. This 
was in Galleries.Components.Picture:

<pre><span style="COLOR: gray">/// <summary>
</summary></span><span style="COLOR: gray">/// This static method gets the location of the picture cache directory, mapped on the local filesystem.
</span><span style="COLOR: gray">/// 
</span><span style="COLOR: gray">/// <returns>string</returns>
</span><span style="COLOR: blue">public</span> <span style="COLOR: blue">static</span> <span style="COLOR: blue">string</span> CacheDirectory()
{
	Uri uri = <span style="COLOR: blue">new</span> Uri(GalleryUrls.Instance().PictureCache);
	<span style="COLOR: blue">return</span> CSContext.Current.Context.Server.MapPath(uri.AbsolutePath);
}</pre>

After that, everything seems to be running as normal. I don't know if I'd 
recommend doing something like this on your install, especially if things are 
working well enough for you. I just use this particular feature of the Metablog 
API quite often, so it bit me a lot.

<p><font color="red">update</font>: It looks like the trackback feature uses fully 
qualified urls as well as the rss/atom feeds. I'll post a fix tomorrow when I 
find out where the BaseUrl is set for the trackbacks.</p>

<p><font color="red">update2</font>: Found it :) I would've got it done last 
night, but I don't have the broadband yet. Any ways, like I thought it was just 
a removal of a baseUrl parameter (case notwithstanding). I found this in 
Blogs.Controls.TrackbackMarkup:</p>

<pre><span style="COLOR: blue">protected</span> <span style="COLOR: blue">override</span> <span style="COLOR: blue">void</span> Render(HtmlTextWriter writer)
{
            
    <span style="COLOR: blue">if</span>(IsValid)
    {
        <span style="COLOR: blue">string</span> baseUrl = Globals.HostPath(Context.Request.Url);
	writer.WriteLine(tag,<span style="COLOR: green">/*baseUrl+*/</span>PermaLink,Title,<span style="COLOR: green">/*baseUrl+*/</span>PingUrl);
    }
}</pre>

<p class="media">[ Currently Playing : Rooster - Alice in Chains - Unplugged 
(6:40) ]</p>