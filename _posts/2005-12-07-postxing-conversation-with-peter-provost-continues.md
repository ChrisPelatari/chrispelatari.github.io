---
layout: post
title: PostXING conversation with Peter Provost continues...
date: 2005-12-07 21:07
author: chrispelatari
comments: true
categories: [professional_geek]
---

<p><a href="http://www.peterprovost.org/">Peter </a>gives me some <a href="http://www.chrisfrazier.net/blog/archive/2005/11/14/1413.aspx#1429">awesome 
feedback</a>: </p>
<blockquote style="margin-right:0;">
  <p>Hey man. Glad to know you're listening. I really think that PostXING could 
  rock with a little more TLC. You're doing great. <br /><br />A few comments on 
  your comments: <br /><br />1. I don't think you understand my request. Assume for 
  a second that I know that I want to open post ID 117, I should be able to 
  "Open 117" instead of "open, browse, wait, wait, 117, OK". I know this can be 
  done with MWAPI 'cause I wrote one. metaWeblog.getPost takes postid, username 
  and password, right? <br /><br />2. For categories, I want to be able to select 
  the category(s) for the post quickly and without waiting for stuff. So cache 
  them, let me reload the cache, and enabled me to select them with the keyboard 
  without a lot of fuss. BlogJet is pretty good on this front. <br /><br />3. I 
  understand your choice here, but I think you would be better to choose the 
  standard keystroke used by Outlook, FrontPage, BlogJet, etc: Ctrl+M and 
  Ctrl+Shift+M. Not the best keystrokes in the world, but they are what people 
  are used to. <br /><br />4. Make all the keystrokes configurable! :) That solves 
  many/all of my issues., eh? <br /><br />5. What I'm saying is that after using 
  Ctrl+K (which I realize is a MSHTML command), and the focus returns back to 
  the app, the input focus should stay where it was. I suspect you have 
  something going on in Form_Activate that sets the focus somewhere. Try it, 
  you'll see what I mean. <br /><br />6. Ctrl+Enter should be Post &amp; Publish. 
  Personally I don't think Post (w/o Publish) has any value at all. If I can 
  save locally, I don't need to post without publishing. <br /><br />Thanks! Keep up 
  the good work!</p></blockquote>
<p dir="ltr">We sure like lists, eh? :) Here's mine in response again:</p>
<ol>
  <li>
  <div>This can be done, absolutely. (meaning I understand now ;) Maybe a 
  command that just loads a post into the editing surface? </div>
  </li><li>
  <div>This is something I've actually had on the plate for a long time that 
  will probably never make it into v1 of <a href="http://postxing.net">PostXING</a>. Since I'm working on v2, tho, it can 
  definitely make it into that code. This will also improve the offline story 
  (currently falls back to an empty textbox where each category gets its own 
  line.)</div>
  </li><li>
  <div>Sounds good, definitely will look into this one too.</div>
  </li><li>
  <div>Wow, that sounds like a lot to do...how many keystrokes should be 
  supported, how could I map them to logical commands, should it be per-user? 
  Lots of questions on that one, I had never thought of doing something like 
  this before.</div>
  </li><li>
  <div>I actually got a tip from Dmitry (creator of BlogJet) on how to deal with 
  this issue. Apparently, mshtml has a focus issue that needs to be explicitly 
  handled.</div>
  </li><li>
  <div>Consider it done.</div></li></ol>
<p>Thanks again, Peter. Sorry it took so long for me to reply, but my 
CommunityServer install is not sending me emails when I get comments :( 
</p>
