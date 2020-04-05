---
layout: post
title: RE&#58; SecurePasswordTextBox update
date: 2006-03-14 21:25
author: chrispelatari
comments: true
categories: [professional_geek]
---

<p>This looks interesting. I thought Mr. "<a href="http://weblogs.asp.net/pglavich/archive/2006/03/12/440050.aspx">Just
finished my last chapter of Beginning AJAX</a>" would have for sure created this
as an asp.net control...guess I should have read closer the first time ;) Could
be useful in <a href="http://postxing.net">PostXING</a>, ifn we ever put some
real security innit.</p>
<blockquote>
  <p>Since there has been so much interest in the SecurePasswordTextBox control
  (see my previous post <a href="http://weblogs.asp.net/pglavich/archive/2006/02/26/439077.aspx">http://weblogs.asp.net/pglavich/archive/2006/02/26/439077.aspx</a> and
  <a href="http://weblogs.asp.net/pglavich/archive/2006/03/12/440052.aspx">http://weblogs.asp.net/pglavich/archive/2006/03/12/440052.aspx</a> ),
  I thought I would take the time to iron out the bugs. When I first released
  it, I performed minimal testing (i.e. about 15 minutes worth) and just thought
  if anybody else is interested, then I might put some real effort in.</p>
  <p>Well since then it was featured in an <a href="http://blogs.msdn.com/dansellers/archive/2006/03/08/546679.aspx">MSDN
  webcast by Dan Sellers </a>of Microsoft and I have received almost 300
  downloads in a short span of time. So just as a quick courtesy note, it has
  now been updated to V1.1 and works (AFAIK) 100%. Previous versions didn't
  handle certain situations property where text in the middle was selected and
  you typed a character, it would simply append the char and not do a
  replacement (thanks Nick :-) )</p>
  <p>All is now well. Go grab it from <a href="http://www.theglavs.com/DownloadItem.aspx?FileID=46">here</a><a href="http://www.theglavs.com/DownloadItem.aspx?FileID=46">http://www.theglavs.com/DownloadItem.aspx?FileID=46</a></p>
  <p>For those unaware, its a Windows Forms TextBox control that uses the .Net
  V2 SecureString class to store its contents. Basically, you now have a UI
  control that allows directly entry into this secure string class and makes it
  useable from a windows UI perspective. (See my <a href="http://weblogs.asp.net/pglavich/archive/2006/02/26/439077.aspx">previous
  post</a> for a full explanation.)</p></blockquote><i>[Via <a href="http://weblogs.asp.net/pglavich/archive/2006/03/14/440191.aspx">Glavs
Blog</a>]</i>
