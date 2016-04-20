---
layout: post
title: PSKit&#58; FormView initial thoughts
---
<p><a href="http://bluefenix.net/">I've been playing with the Personal Website 
Starter Kit a little bit lately</a>. One thing that I didn't like about it from 
the start was that the content in the default.aspx was largely static, so I set 
out to make it a little more dynamic. After a little digging in the <a href="http://beta.asp.net/QUICKSTARTV20/aspnet/doc/ctrlref/data/formview.aspx">whidbey 
quickstarts</a> I decided that a FormView <strike>would 
be</strike> looked like the way to go.</p>
<p>I'm trying to keep any modifications simple, so I created a really simple 
table that would cover the very basic needs of the sections that are shown 
on the default.aspx:</p>
<p><u>Content<br /></u>ContentID<br />Heading<br />Content<br />IsVisible</p>
<p>I then created the basic CRUD procedures that would go with this table, 
dropped a FormView onto the default.aspx, and created a SqlDataSource to supply 
it with data. Now, let me say that it is very...what's the word? liberating? to 
be able to do most of the work in the designer without worrying about the 
designer nuking stuff. It's almost there. One thing that I thought was missing 
was the ability to specify one of the connectionStrings from the web.config file 
as the connection string source - you've got to switch to source view to do that 
(afaict). Also, the friggin thing doesn't want to work unless I supply a 
DefaultValue for each &lt;asp:ControlParameter/&gt; in the markup - so what 
happens when my ID changes?</p>
<p>One other thing that I'd like to see (I know, give an inch, take a mile:) 
would be the ability to use the same SqlDataSource for many FormViews. As the 
default.aspx is laid out now, there are 3, maybe 4 areas that would be good 
candidates for being populated from the <u>Content</u> table outlined above. So 
if I had FormView2, FormView3, and FormView4, I would like to associate them all 
with the same SqlDataSource and vary the output based on a different ContentID 
for each. Right now, it seems like there is a 1:1 mapping between each 
SqlDataSource and FormView (as the ControlParameter has a ControlID associated 
with it.) Maybe I should try using a different type of parameter? </p>
<p>More to come...I'll get this eventually :)</p>