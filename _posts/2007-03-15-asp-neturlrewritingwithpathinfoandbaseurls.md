---
layout: post
title: ASP.NET - UrlRewriting with PathInfo and base urls
date: 2007-03-15 13:45
author: chrispelatari
comments: true
categories: [Uncategorized]
---

<p>I read <a href="http://weblogs.asp.net/scottgu/archive/2007/02/26/tip-trick-url-rewriting-with-asp-net.aspx">this 
excellent post from ScottGu </a>and decided to use it with a page that 
implemented a masterpage. I didn't have to use postbacks in my scenario, but 
there were links included from the masterpage. The problem is that if you use 
app-relative paths for your href attributes (ex: &lt;a href="/default.aspx"&gt;) 
the browser (FF 2.0.0.2 and IE 7 anyways) interperets the url with pathinfo 
differently than a url without. The base url includes the original page (ex: <a href="http://localhost:3333/rewriter.aspx/default.aspx">http://localhost:3333/rewriter.aspx/default.aspx</a>). 
Guess what? The webserver picks up the last .aspx extension, 
default.aspx, that bad boy doesn't exist, and you get a 404 instead of 
going to <a href="http://localhost:3333/default.aspx">http://localhost:3333/default.aspx</a>.</p>
<p>In the comments, Ian Oxley suggested that you can re-base links in your 
page/css/other static files using the &lt;base&gt; element in the head of your 
page. I expanded on it a little, since this behavior is only on one page of my 
site currently, and added the following code into the Page_Load event of the 
offending page:</p><pre><span style="color:blue;">this</span>.Header.Controls.Add(
<span style="color:blue;">new</span> LiteralControl(<span style="color:maroon;">"&lt;base href=""</span> +
 Request.Url.ToString().Replace(Request.RawUrl, <span style="color:maroon;">""</span>).Replace(Request.PathInfo, <span style="color:maroon;">""</span>) + 
<span style="color:maroon;">""&gt;"</span>));</pre>
<p>Now the base tag works on both the live site and the one that 
WebDev.WebServer spins up as well.</p>
<p class="media">[ Currently Playing : Them Bones - Alice in Chains - Nothing 
Safe: Best of the Box (2:29) ]</p>
