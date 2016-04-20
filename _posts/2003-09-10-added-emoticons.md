---
layout: post
title: added emoticons :)
---
<p>I've recently added emoticons<img alt="Smiley" src="/blog/images/emotions/emotion-1.gif" border="0" />to my .Text blog. If you could see the code, it <a href="http://www.asp.net/Forums/Download/Default.aspx?tabindex=0&amp;tabid=1" target="_new">might look familiar</a>. Heh, that was pretty easy. I did make a change or two to the source of .Text and also added a key to the web.config's appsettings node.</p>
<p>The magic happens in a method called StripFTB (for free textbox, the editor used for this app) All I did was add a call to the new Transform class, added the appropriate text file, and we're in business.</p>
<p>If you haven't checked it out yet, .<a href="http://scottwater.com/dottext" target="_new">Text</a> is a real good app - it's been real easy to make changes to it to 'fit my needs'.</p>