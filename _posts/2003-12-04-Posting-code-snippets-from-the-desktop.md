---
layout: post
title: Posting code snippets from the desktop...
---
[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml) told me:

>Feature request: you will be my hero if your blog software can display code snippets in a color coding like in VS.NET. And if it's a snap to add such code and have it formatted. (That is, I don't have to do more than just add, \[code language="C#"\] ... code ... \[/code\].) 

Thanks to [Thomas Johansen's](http://weblogs.asp.net/tjohansen) [AylarSolutions.Highlight](http://aspalliance.com/aylar/highlight/), you're gonna get exactly that!

This was one of the requests that more than one person told me would be nice, so I decided to go ahead and add syntax highlighting to the app b/c yeah it would be nice. Tom's component makes it sickeningly easy to highlight C#, VB.NET, J#, and I believe recently he even added ASPX support.

Initially I was thinking that a 'snippet dialog' would be the easiest way to accomplish this, just insert where the cursor is on the editing surface. Then I thought, well, if I can wrap a font tag around some words that I highlighted, then I should be able to do the same with the syntax highlighting markup, just add a button with a language dropdown to the [toolbar](http://www.divil.co.uk/net/controls/sandbar/), highlight the code you want to show the syntax for, click 'codify' and go!

Now, ScottM is mentioning some custom markup syntax, familiar to anyone who has posted on an online forum. So, you would have a region that you know *will* look like VS.NET's scheme when it's posted to the blog, but the only visual clue you'll have is the custom markup around the code - it won't be syntax highlighted until you hit the Post &amp; Publish button.

So which would you prefer - from an end user's standpoint? What would make you say, “Yo, that's super easy to add code to my posts“?