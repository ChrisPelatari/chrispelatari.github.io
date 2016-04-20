---
layout: post
title: ImageLists
---
<p>Looks like <a href="http://weblogs.asp.net/mlafleur/">Marc </a>is <a href="http://weblogs.asp.net/mlafleur/posts/27017.aspx">having trouble with sealed ImageLists</a>.</p>
<p>I've been working on my first Windows Forms project and I'm using the same ImageList throughout the application, even tho there are yet only a few forms in it. I adapted an example by Lutz Roeder that uses a static class (well, ya know static members, whatever) to load a bitmapstrip into an internal ImageList. The class has a bunch of static properties that return the correct index of the image based on the loaded ImageList. (Like Images.Forward or Images.Undo)</p>
<p>I also added a static property to return the internal ImageList incase I want to use it in one of my Forms without calling the individual properties.</p>
<p>The trick is to load the bitmap strip in a static constructor - it's <em>always</em>  called first. If I want to add an individual image to a form, I can either create a local ImageList and set it to Images.ImageList or simply set the image of the control I'm targeting to say Images.Back. I have to admit, I usually add the image in (gasp) the InitializeComponent() call - but here's the nice part: since I'm calling a completely static class, the designer can get to the images and loads it not only to the designer surface but also (usually) replaces my Images.Back call with an appropriate call to the ResourceManager to grab the image from its new home - my Form's .resx file. </p>
<p>Good luck, Marc.</p>