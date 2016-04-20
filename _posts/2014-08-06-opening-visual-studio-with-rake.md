---
layout: post
title: Opening Visual Studio with Rake
date: 2014-08-06 21:13
author: chrispelatari
comments: true
categories: [rake, Uncategorized, visual_studio]
---
There are probably several ways to do this, here’s how I did.</p>

rakefile.rb:<br><font style="background-color:#666666;" color="#00ff00" face="Consolas">DIR = File.dirname(__FILE__)<br>desc "Starts Visual Studio with the project solution."<br>task :vs do<br>&nbsp; sln = "#{DIR}/src/project.sln".gsub! '/','\\'<br>&nbsp; system( "start #{sln}" )<br>end</font>

That’s it! From a cmd shell type “rake vs” and Visual Studio will start with the specified solution file.
