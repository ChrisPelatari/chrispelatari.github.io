---
layout: post
title: "If I only knew then..."
---
 
<p>Not what I <strong>know</strong> now, but what I'm <strong>learning</strong> 
now. I recently picked up a copy of the src to <a href="http://www.flexwiki.com/default.aspx/FlexWiki/FlexWikiPad.htm">FlexWikiPad</a>. 
I just wanted to see how things were wired together in there: I only have a very 
old installation of FlexWiki sitting around that still looks like crap in 
FireFox.</p>
<p>To his credit, <a href="http://pluralsight.com/blogs/craig">Craig </a>has 
done an awesome job of making FlexWikiPad very testable - something I didn't 
think was all that easy to do in winforms. Apparently, his dialogs are very 
humble. He's using a pretty strict <a href="http://www.martinfowler.com/eaaDev/ModelViewPresenter.html">Model View 
Presenter </a>(or controller, whatever) pattern throughout the application. I 
thought this was a lot of extra coding at first (it kinda is), but in the 
process Craig has made FlexWikiPad easier to maintain and update thru the use of 
mocks/stubs and tests with this pattern.</p>
<p>Currently, I've got this itch that I want to scratch with regards to <a href="http://PostXING.url123.com/main">PostXING</a> that would have been so 
nice to be able to test my way thru. I'm just hacking thru it now, and I've 
done a pretty good job of messing everything up so far :) In my 
defense, I'm still learning unit testing and when it comes to winform 
applications I feel that there is a balance that I like to hit right on the line 
of usability and architectural beauty. Anyone who has looked at PostXING's 
source will soon see that my architectin' ain't so purty - it's still just a lot 
of different pieces from different places glued together. I don't validate 
everything that I should. I left fields that I <em>intended </em>to add 
functionality for disabled but visible. Even up to 1.1 versions. 
<strong>BUT</strong>...</p>
<p>...and this is a big but...</p>
<p>...it works. That was priority #2 for me with PostXING. Priority #1 was to 
make something useful that I could use to learn winforms. </p>
<p>Anyways, I'm hoping that I can glean some insight off of people like Craig 
that are way more knowledgable than me on this front. If I feel like the task 
for PostXING to be testable is too great, I may just try to apply this knowledge 
to future projects. So, thanks Craig for making FlexWikiPad follow a concise 
pattern that I did know about but have never seen implemented with tests in C# 
before.</p>