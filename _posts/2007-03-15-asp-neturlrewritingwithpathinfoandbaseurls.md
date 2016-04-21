---
layout: post
title: ASP.NET - UrlRewriting with PathInfo and base urls
date: 2007-03-15 13:45
author: chrispelatari
comments: true
category: aspnet
---

I read [this
excellent post from ScottGu](http://weblogs.asp.net/scottgu/archive/2007/02/26/tip-trick-url-rewriting-with-asp-net.aspx) and decided to use it with a page that
implemented a masterpage. I didn't have to use postbacks in my scenario, but
there were links included from the masterpage. The problem is that if you use
app-relative paths for your href attributes (ex: &lt;a href="/default.aspx"&gt;)
the browser (FF 2.0.0.2 and IE 7 anyways) interperets the url with pathinfo
differently than a url without. The base url includes the original page (ex: [http://localhost:3333/rewriter.aspx/default.aspx](http://localhost:3333/rewriter.aspx/default.aspx)).

Guess what? The webserver picks up the last .aspx extension,
default.aspx, that bad boy doesn't exist, and you get a 404 instead of
going to [http://localhost:3333/default.aspx](http://localhost:3333/rewriter.aspx/default.aspx).

In the comments, Ian Oxley suggested that you can re-base links in your
page/css/other static files using the <base> element in the head of your
page. I expanded on it a little, since this behavior is only on one page of my
site currently, and added the following code into the Page_Load event of the
offending page:

```csharp
this.Header.Controls.Add(new LiteralControl("<base href=\"" +
 Request.Url.ToString().Replace(Request.RawUrl, "").Replace(Request.PathInfo, "") +
"\">"));
```

Now the base tag works on both the live site and the one that
WebDev.WebServer spins up as well.

[ Currently Playing : Them Bones - Alice in Chains - Nothing
Safe: Best of the Box (2:29) ]
