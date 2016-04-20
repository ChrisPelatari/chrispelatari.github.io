---
layout: post
title: "PostXING Answers for Yex"
description: ""
category: 
tags: []
---
 

<p>Yex sez: <!--StartFragment --></p>
<blockquote>
  <p> Nice. So where's the Categories, Post, Post and Publish and Crosspost 
  buttons at? Where's the post editing toolbar? When can we get our grubby 
  little hands on it? <br /><br />Since it appears you've decided to go with the 
  whole sidebar idea, why not use that to list the cateogories checkboxes? Seems 
  logical to me anyway. </p>
  <p class="posteds"><a id="_ctl0__ctl0__ctl0__ctl0__ctl0__ctl0_Comments__ctl0_Comments__ctl0_NameLink" title="Anonymous" href="http://www.chrisfrazier.net/blog/utility/Redirect.aspx?U=http://yexley.net/bob/" target="_blank" rel="nofollow">Yex</a> </p></blockquote>
<p>Good questions! I've actually created a sidebar for the categories, and am 
currently studying a couple of the API's I want to support right away - it looks 
like I will be able to handle categories the same way that I do currently. I'm 
going to try and find a way to push categories into the file that is saved 
(er..File -&gt; Save) for a better offline story too.</p>
<p>I'm also looking to remove the History dialog and replace it with a "view" on 
the main form - no reason other than trying to get rid of unnecessary dialogs. 
And it'll look cool :)</p>
<p>As far as all of the other buttons, my current plan is to have all of that 
plus some configuration details pushed off to a kind of "provider" - each api 
plugin should know what buttons it wants to add, what operations those buttons 
support, what kind of identifying information the api needs, etc.</p>
<p>I'm hoping that I'll be able to break things down to a common denominator and 
have something that will be able to tailor the UI to the current blog that is 
being edited.</p>
<p>And as far as the grubby hands, sorry - it's probably going to be a little 
while before this is ready for prime time. I'm not even ready to dogfood v2 
yet. :( </p>
<p>[ Currently Playing : Would? - Alice in Chains - Unplugged (3:42) 
]</p>