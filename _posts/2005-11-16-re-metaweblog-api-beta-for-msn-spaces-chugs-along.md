---
layout: post
title: RE&#58; MetaWeblog API beta for MSN Spaces chugs along
date: 2005-11-16 06:02
author: chrispelatari
comments: true
categories: [professional_geek]
---

<blockquote>
  <p>Since announcing that we've started
  the beta of our implementation of the <a href="http://www.xmlrpc.com/metaWeblogApi">MetaWeblog API</a> for <a href="http://spaces.msn.com/">MSN Spaces</a>, I've received a bunch of
  positive responses from a couple of blogging tool developers. So far it looks
  like there'll be at least six blogging tools users will be able to use to
  manage the blog on their space after we launch the API. </p></blockquote>
<p><i>[Via <a href="http://www.25hoursaday.com/weblog/PermaLink.aspx?guid=a48f5a69-86e9-4264-ae0b-8f8b39f3baef">Dare
Obasanjo aka Carnage4Life</a>]</i> </p>
<p>Add at least one more - PostXING v2 will work with MSN Spaces via the
MetaWeblog API. I don't think that it will work well with previous versions
because I had to change some code in <a href="http://xml-rpc.net">xml-rpc.net</a> to handle the BOM as I noted
earlier. If the xml-rpc.net library was updated for v1, I'm sure it would work
there as well.</p>
