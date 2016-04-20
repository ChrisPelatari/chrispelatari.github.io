---
layout: post
title: IPlugin implemented.
---
<p>So I ended up working out a method to load plugins - it's a hybrid of Royo's 
<a href="http://weblogs.asp.net/rosherove/archive/2003/11/24/39484.aspx">Extensibility 
Application Block</a> and the method used by <a href="http://rssbandit.org">RssBandit</a>. Now, I do have rudimentary spell 
checking in my dogfood version of PostXING (again :), but I'm having trouble 
figuring out how to handle the dictionary files.</p>
<p>By default, <a href="http://www.loresoft.com/Applications/NetSpell/default.aspx">NetSpell</a> looks 
for a culture-sensitive .dic(tionary) file from the Application.StartupPath (I 
think - when trying to launch <a href="http://PostXING.url123.com/main">PostXING</a> from the <a href="http://PostXING.url123.com/plugin1.0.4365.1">BlogThisUsingPostXINGPlugin</a>, 
it complains that it cannot find the file...\bin\RssBandit\en-US.dic) I manually 
copied the en-US.dic file to PostXING's root folder and it works when launching 
the program by itself. </p>
<p>The thing is that you can specify which dictionary file you want to use in 
the component as well as where that file is located. This would be helpful in 
situations where your CultureInfo is set to something other than English, but 
you mainly post to your blog using the English language. I'm thinking that I 
might be able to address this using something like the IBlogExtension idea of 
HasConfiguration or HasEditingGUI or a combination of the two. This means that 
this part of PostXING is gonna take a little bit longer to finish than I 
originally thought - I want to get it right, ya know?</p>
<p>Also, I don't know how I'm going to handle the distribution of the dictionary 
files - NetSpell comes with these by default:</p>
<p>de-DE.dic<br />en-AU.dic<br />en-CA.dic<br />en-GB.dic<br />en-US.dic<br />es-ES.dic<br />es-MX.dic<br />fr-FR.dic<br />it-IT.dic</p>
<p>with a combined size of nearly 10MB. (The biggest one is de-DE at 2.1Mb). 
There's no way I could host all of these on <a href="http://projectdistributor.net">ProjectDistributor</a> - that would be 
an abuse of a great service. I am so open to ideas on how to address this one 
it's not even funny. The spell checker is pretty well useless without a good 
dictionary file to back it up. Anyways, these are the issues I'm facing while 
trying to get this <a href="http://www.loresoft.com/Applications/NetSpell/default.aspx">great spell 
checking component </a>implemented as a plugin. Happy New Year!</p>
<p class="media">[ Currently Playing : Down in a Hole - Alice in Chains - 
Unplugged (5:45) ]</p>