---
layout: post
title: ObjectDataSource goodness.
---
<p>Since there are probably going to be a lot of posts about all things 
Whidbey soon, as people get more and more chance to play with things, I've 
decided to throw in my two cents about a really cool piece of functionality that 
I recently used.</p>
<p>ObjectDataSource - too cool, I've been waiting for something like this for a 
while. This is more my style than using stinkin' DataSets. You can see what I 
did at <a href="http://bluefenix.net/projects.aspx">bluefenix.net</a> . I 
built it based off of the Personal Site Starter Kit that comes with vwd on up, 
so there's still a lot of Lorem Ipsum text in there. Well, pretty much the whole 
site is Lorem Ipsum text right now, except for the Projects.aspx page.</p>
<p>The page consists of two DataLists, an ObjectDataSource and a SqlDataSource. 
For the ObjectDataSource, all I did was add a web reference to the website and 
point the SELECT part of the datasource to the method that had the info that I 
wanted to display. That worked off my local machine perfectly, but I needed to 
go thru a proxy at the host to make the webservice work correctly. Getting this 
working was a simple matter of creating a wrapper to the webmethod that included 
adding proxy info to the webservice stub class before calling the webmethod. 
Changing the ObjectDataSource's SELECT section to use the new class that was 
dropped into App_Code got everything working, locally and in production!</p>
<p>Very cool, indeed.</p>
<p class="media">[ Currently Playing : Imagine - A Perfect Circle - eMOTIVe (4:48) 
]</p>