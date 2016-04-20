---
layout: post
title: Getting Started on some Controls Issues
tags: ASP.NET-WebControl-Development
---
<P>I decided to go ahead and try to start building something in the control arena - something I haven't visited for some months now. </P>

<P>I figured it would be a good idea to start with a pretty solid idea - the rollover image link. I'm using <A href="http://metabuilders.com/Tools/RollOverLink.aspx">Andy Smith's RollOverLink</A>&nbsp;as kind of a starting point - see one of our normal requirements at work is to display a statusbar message when an image link is 'moused over', so I figured I'd add this as another property of Andy's great control. Thanks for the kick start, Andy! </P>

<P>next, I think I'm going to add a configurationSectionHandler, based very loosely on the config handler of the ExceptionManagement ApplicationBlock - meaning I want to take an attribute oriented approach to populating the various properties of my control. </P>

<P>I guess I should mention that I got this idea for a particular splash page that govern a lot of the web apps that I put together, so the config section will probably be specific to that app, while the control I might just start using all over the place. </P> 