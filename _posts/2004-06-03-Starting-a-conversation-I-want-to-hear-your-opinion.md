---
layout: post
title: Starting a conversation - I want to hear your opinion.
---
<p>I wanted to ask for your opinion. I've been building this little wysiwyg 
blog-posting tool for a little bit. I call it PostXING, and I'm using it right 
now to post this very message. It is inspired by a tool that <a href="http://scottwater.com">ScottW</a> wrote called Blogert. For the 
wysiwyg abilities, it uses an interface to mshtml. </p>
<p>Where I could, I tried to keep the default dialogs (like hyperlink, image, 
etc) for use in the app. So, when adding an image using the default dialog, if 
you're adding it from your machine you get a path like "C:\myimages\img.gif" 
when you really want something like " http: / /mysite.com/img.gif " (sans 
spaces, of course). This app has an idea of "FTP sites" for each blog you 
might have configured. So I was thinking that, provided the "FTP site" was 
configured for your blog, it would just try to upload each image found. 
</p>
<p>So far I'm just thinking out loud, setting this up for you to give me your 
opinion if you so choose. I'm trying to figure out if there are any 
gotchas I'm not thinking of. For example, I would only want this to happen when 
a post is first added to begin with - this presumes that if you're updating a 
post, the images are already there. Fair enough, right? Also, I never plan to 
port this thing to Mono/Gtk# or whatever, so I could pretty much rely on 
finding " :\ " or simply <br />" \ " , right? And when cross-posting 
comes into play, how should I control things then? I mean, I have two blogs, but 
it makes sense to upload the images to only one of them, then replicate the new 
and improved html over to the cross-posted blog. Is there anything I'm not 
thinking of here?</p>
<p>If you've read this far, thanks. I'm not gonna get all "political" with this 
tool. It's not trying to be "better" than anybody else's tool. If I ever 
"release" it, it'll be totally free (BSD-style). I started building this tool 
because I had an immediate need to be able to cross-post the same content to 
different blogs selectively. I wanted to see what I could do with windows forms 
by making something practical to use that didn't cost me anything but a little 
free time. Thanks again for reading this, and your constructive opinions are 
welcome.</p>