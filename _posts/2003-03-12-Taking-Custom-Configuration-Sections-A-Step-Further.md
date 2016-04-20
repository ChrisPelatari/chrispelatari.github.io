---
layout: post
title: Taking Custom Configuration Sections A Step Further
tags: ASP.NET-WebControl-Development
---
>*Yup, it's cool, but it gets __even cooler__ when you start writing your own configuration section handler implementations. The beauty of the configuration architecture is that it's completely extensible.*

>\[[From Drew's Blog](http://dotnetweblogs.com/dmarsh/)\]

>>Thanks Drew.&nbsp; I kinda figured I'd only scratched the surface with this stuff.&nbsp; Thanks, I'm gonna check out IConfigurationSectionHandler stuff

>>\[Currently Playing: Rancid - Life Won't Wait\]

>>\[[.NET Brain Droppings](http://dotnetweblogs.com/DBrowning/posts/3708.aspx)\]

BAM! I did it - I knew it could be done, but I had no idea how simple the 
framework makes it. I'm talking about hydrating a list of the hyperlink controls 
I recently created from a config file using a custom config section handler - 
I'll write a story on how I got it done here shortly. Well, tonight anyway. 

Basically, I used a method near what Drew described, but I took an 
attribute-based approach - so the web.config has a section that looks like a 
list of server controls without the &lt;asp: at the beginning. 
<EM><FONT color="royalblue">\[Hearing : System Of a Down : Jet 
Pilot\]</FONT></EM>