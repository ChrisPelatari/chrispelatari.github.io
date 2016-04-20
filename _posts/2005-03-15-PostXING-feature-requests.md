---
layout: post
title: PostXING feature requests
---
<p><a href="http://blog.lotas-smartman.net/archive/2005/03/15/11201.aspx">Teirnan 
asked for a few features for PostXING</a>. I started to write a comment, but it 
got too long-winded for a comment. You get a post Sir:</p>
<p>Can I help you? I think maybe so :) In order:</p>
<ul>
  <li>I did this in a very early build of PostXING, but got some feedback that 
  asked to be able to immediately edit the post that was just, erm, posted - in 
  case of typos or whatever. I guess I could make it configurable, that 
  shouldn't be too hard. Since you are literally the first person to ask for 
  this feature, I think I'll make the current behavior the default. 
  </li><li>I don't know how to tackle this one - PostXING is basically just a wrapper 
  for <strong>SOME</strong> functionality of the Metaweblog API. Generally, the 
  blog engine will handle the entry IDs. Sometimes it gives you an int, 
  sometimes it gives you a string. 
  </li><li>I actually tried to do this at one point, but I'm not sure how stable it 
  would be. Think about it this way: in order for this to work, images would 
  have to be parsed out (not a problem) and each one uploaded one at a time 
  using the FTP component. The resulting url would have to be pumped back into 
  the post and then and only then could you finally post/publish the entry. If 
  you have a lot of images, this could take a really long time and thus give the 
  perception that PostXING performs poorly. I guess I could make this a config 
  option too with the caveat that it could possibly take a really long time to 
  make a post. 
  </li><li>This one is easy :) If you want it to be zippy, download the latest 
  version of Vault from <a href="http://vaultpub.sourcegear.com">http://vaultpub.sourcegear.com</a> . 
  Login as the guest account (I think it's guest/guest) and go to the PostXING 
  repository. Set a working folder and click Get Latest Version. The latest code 
  release should be there, although it may be a little out of sync with the most 
  current version that I'm dogfooding on my local machine. You can also find any 
  plugins code that is associated with PostXING. If you don't want to install 
  vault for whatever reason, I'm pretty sure you can download from their web 
  interface using the same uid/pwd, but I'm sure it would be about 100 times 
  more painful.</li></ul>
<p>Thanks for the feedback, Tiernan. </p>
<p class="media">[ Currently Playing : I'm done - Korn - Take a look in the mirror 
(3:23) ]</p> 