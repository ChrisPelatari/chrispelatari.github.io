---
layout: post
title: RE&#58; PostXING Review - Yet Another Blog Posting Client
date: 2005-11-15 00:56
author: chrispelatari
comments: true
categories: [professional_geek]
---

<p>Ah! It's been a while since I've gotten some good PostXING feedback. Guess
the current version isn't very keyboard-friendly. I'm probably not going to
upgrade the v1 code in v1 of .net, but I've been working for the past couple of
weeks on getting PostXING to v2 under .net v2, so none of these requests are out
of the question. As a matter of fact, I welcome all criticism in the hopes of
making PostXING a product that works really well for more than just myself.
Anyways, <a href="http://www.peterprovost.org/archive/2005/11/13/9511.aspx">Peter</a> has
some good feedback for PostXING in general, my responses follow his post:</p>
<blockquote>
  <p dir="ltr" style="margin-right:0;">I decided today to try out <a href="http://projectdistributor.net/Projects/Project.aspx?projectId=12">PostXING</a>
  as an alternative to <a href="http://blogjet.com/">BlogJet</a>. So far my
  reaction is mixed.</p>
  <p dir="ltr" style="margin-right:0;"><strong>Pros</strong></p>
  <ul>
    <li>
    <div style="margin-right:0;">Seems to have good WYSIWYG support</div>
    </li><li>
    <div style="margin-right:0;">I like having the standard HTML heading tags
    available in the toolbar.</div>
    </li><li>
    <div style="margin-right:0;">I can easily insert a horizontal rule in my
    post</div>
    </li><li>
    <div style="margin-right:0;">I <u>love</u> the fact that it has the <a href="http://puzzleware.net/codehtmler/default.aspx">CodeHTMLer</a> syntax
    hilighting engine in it, but it doesn't feel quite as smooth to me as
    BlogJet does.</div>
    </li><li>
    <div style="margin-right:0;">I'm very glad that it supports uploading
    images via FTP in the same way that BlogJet does. This is a must have in my
    book.</div>
    </li><li>
    <div style="margin-right:0;">As with BlogJet, I can't open an arbitrary
    post by ID. I have to find it in the historical list of posts, which sucks
    when the post is from a year ago.</div></li></ul>
  <p style="margin-right:0;"><strong>Cons</strong></p>
  <ul>
    <li>
    <div style="margin-right:0;">I have to click a button and wait for a popup
    to set the post's categories</div>
    </li><li>
    <div style="margin-right:0;">I can't use TAB to navigate the UI
    which means I have to use the mouse (a serious usability error as far as I'm
    concerned). And I don't know if I agree with the idea that TAB causes
    BLOCKQUOTE in the resulting HTML.</div>
    </li><li>
    <div style="margin-right:0;">I can't find keystrokes for many of the
    standard formatting things like ordered and unordered lists, styles,
    etc.</div>
    </li><li>
    <div style="margin-right:0;">Sometimes after using CTRL+K to format some
    text as a link (good), the input focus leaves the text editor and goes up to
    Title field (bad).</div>
    </li><li>
    <div style="margin-right:0;">I can't figure out how to post with a
    keystroke. It should be CTRL+Enter (like Outlook and BlogJet) but it
    isn't.</div></li></ul>
  <p dir="ltr" style="margin-right:0;">This will be my first post with it, we'll
  see if it is also my last. If the author can fix a few of those cons, I would
  be considering switching. For now though, I'm not so sure.</p>
  <p dir="ltr" style="margin-right:0;">This seems like such a simple problem...
  I can't believe how poor all the choices really are.</p>
  <blockquote style="margin-right:0;">
    <p><img height="1" src="http://www.peterprovost.org/aggbug/9511.aspx" width="1" /></p></blockquote></blockquote>
<p><i>[Via <a href="http://www.peterprovost.org/archive/2005/11/13/9511.aspx">Geek
Noise</a>]</i> </p>
<p>I'll try to address these as best I can, starting with the last Pro...</p>
<ul>
  <ul>
    <li>This is a drawback of the MetaWeblog API, which is why you see the same
    behavior across both BlogJet and <a href="http://PostXING.url123.com/main">PostXING</a>. The only way to really
    get around this is to use a different API to access your blog, like perhaps
    the webservice API in CS. Hopefully when CS v2 drops I'll be able to code up
    a plugin/provider that allows native access to the webservice api instead of
    having to use mwb all the time.
    </li><li>In v2, the popup is replaced with a "Container Bar", but it's still the
    same concept. How would you rather see the category feature implemented?
    Perhaps as a dropdown next to the title kind of like w.bloggar?
    </li><li>PostXING does capture the tab key in the editor surface to create a
    blockquote: I did this to be able to format quotes quickly. Maybe it was a
    wrong decision, but this is the first time that I've ever heard anything bad
    (if a Con is bad) about it. I could for sure make this configurable, but
    what should the default behavior be? Insert 4 spaces, or be able to tab
    around the rest of the application? I guess at the time that I implemented
    the tab capture, I figured the editor experience was the main focus of
    PostXING.
    </li><li>You can't find these keystrokes because they don't exist. What should
    they be?
    </li><li>This is 100% mshtml code (especially the ctrl+k part). I don't know how
    to address this but like all of the other points I'm open to suggestion.
    </li><li>Again, there is no keystroke for this. Sorry. :( I will for sure add
    ctrl+Enter support, but which button should this be associated with? Post or
    Post &amp; Publish?</li></ul></ul>
