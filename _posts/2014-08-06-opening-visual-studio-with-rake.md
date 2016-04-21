---
layout: post
title: Opening Visual Studio with Rake
date: 2014-08-06 21:13
author: chrispelatari
comments: true
categories: [rake, visual_studio]
---
There are probably several ways to do this, here’s how I did.

rakefile.rb:

```ruby
DIR = File.dirname(__FILE__)
desc "Starts Visual Studio with the project solution."
task :vs do
 sln = "#{DIR}/src/project.sln".gsub! '/','\\'
 system( "start #{sln}" )
end
```

That’s it! From a cmd shell type “rake vs” and Visual Studio will start with the specified solution file.
