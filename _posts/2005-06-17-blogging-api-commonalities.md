---
layout: post
title: "Blogging API commonalities"
description: ""
category: 
tags: []
---
 

<p>Here is some of the common ground I can see between the metaweblog api and 
CS::Blogs BlogService asmx.</p>
<p>Blog/Authentication:</p>
<ul>
  <li>UserName</li>
  <li>Password</li>
  <li>BlogID/BlogName</li></ul>
<p>Post/Entry:</p>
<ul>
  <li>DateCreated/Date</li>
  <li>Description/Body</li>
  <li>Title</li>
  <li>string[] Categories (nice!)</li>
  <li>PostID</li></ul>
<p>Non-Conformities (for Posts):</p>
<ul>
  <li>Metablog API</li>
  <ul>
    <li>Enclosure (although this is not used by CS::Blogs or .Text)</li>
    <li>link</li>
    <li>permalink</li>
    <li>Source (name and url, was supported by .Text, not so sure about 
    CS::Blogs)</li>
    <li>userid</li></ul>
  <li>BlogService.asmx</li>
  <ul>
    <li>Excerpt</li>
    <li>Name (I guess this is for url rewriting)</li>
    <li>Enable Comments</li>
    <li>Enable Trackbacks</li>
    <li>Moderate Comments</li>
    <li>Enable Ratings</li>
    <li>Syndicate</li>
    <li>Syndicate Excerpt (I guess you have to define an excerpt for this to 
    work?)</li>
    <li>Syndicate Root (for communities?)</li>
    <li>DisplayOnHome (again, communities?)</li>
    <li>IsArticle (I really dig this one. I've wanted to be able to edit 
    articles from the desktop for a long time.)</li></ul></ul>
<p>I've also been looking at ATOM a little bit - there doesn't seem to be any 
mention of categories in atom, which kinda sucks considering categories are a 
nice way to filter content.</p>
<p>All of the apis, including atom, have one other thing in common: getting 
general blog information is usually a two-step process. As an end user, I must 
supply a username, a password, and a url (although the atom api lets you enter a 
homepage url with a &lt;link/&gt; element that points to the service url (v1.0 
of CS::Blogs asks for a blogname, too. Maybe this says that you should only work 
with one blog at a time?)). Then I get a list of blogs that I can edit with the 
credentials supplied. Then I can create, update, or delete a post. I can also 
get a list of recent entries (and articles in the case of the BlogService.asmx). 
</p>
<p>With atom, on blogger at least, you are required to use https:// as the uri 
scheme. Not a big deal, this just means that the common denominator for a blog 
has to have a couple of booleans: UseSSL and SupportsCategories, because those 
two are what separates atom and the apis of CS::Blogs from a coding standpoint. 
Since I'm going to be using libraries to handle the xml transfers (xml-rpc, 
soap, or rest) I could care less what the xml looks like.</p>
<p>Speaking of libraries, the code that I have for handling the metaweblog api 
also includes support for the old blogger xml-rpc api (thanks, dasBlog!), so 
I'll probably include support for posting to that api as well in the new version 
of <a href="http://PostXING.url123.com/main">PostXING</a>.</p>