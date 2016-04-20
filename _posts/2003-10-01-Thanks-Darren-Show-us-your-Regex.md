---
layout: post
title: Thanks Darren...Show us your-Regex!
---
<p><a href="http://www.velocitydatabank.com">The place that I work </a>uses what we call index numbers (they're not really numbers per se...) that are based on API numbers (which are usually numbers) for check shot velocity surveys. I'm working on a project that will validate these and I thought that it would be well suited for Regex since it's going to be text validation and there are rules in place for these Index “numbers”. </p>
<br />
<p>So first I go to <a href="http://www.regexlib.com">www.regexlib.com</a> and see what that might have to get those Regex juices flowin. Then I thought about the Regex that I need to write and wrote it out as the rules should apply:</p>
<br />
<ol>
<br />
<li>Start at the beginning of a string.</li>
<br />
<li>Match exactly 2 digits.</li>
<br />
<li>Match exactly 1 letter (uppercase).</li>
<br />
<li>Match no less than 3 but no more than 4 digits.</li>
<br />
<li>Optionally match 1 or 2 letters (uppercase).</li>
<br />
<li>End of string.</li></ol>
<br />
<p>So, I fired up <a href="http://weblogs.asp.net/DNeimke">Darren Neimke's</a> <a href="http://www.gotdotnet.com/Community/UserSamples/Details.aspx?SampleGuid=43D952B8-AFC6-491B-8A5F-01EBD32F2A6C">RegexSnippets</a> which I have sitting in my C:\Tools folder for just such an occasion, and this is what I came up with:</p>
<br />
<p>^\d{2}[A-Z]{1}\d{3,4}([A-Z]{1,2})?$</p>
<br />
<p>And much to my surprise it worked the first time running! Very nice. Plus, I was able to save the regex for later using Darren's cool little utility. Added bonus: there was already one expression (8PointFloat) that I needed for a different area. Thanks Darren!</p>