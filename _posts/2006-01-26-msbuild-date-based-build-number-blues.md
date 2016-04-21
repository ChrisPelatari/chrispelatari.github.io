---
layout: post
title: MSBuild&#58; Date-based build number blues
date: 2006-01-26 21:28
author: chrispelatari
comments: true
categories: [dotnet]
---

According to [this thread](http://forums.microsoft.com/MSDN/ShowPost.aspx?PostID=193986&amp;SiteID=1), Microsoft may run into visioning problems if they stick with their
new build number scheme (major.minor.yMMdd.revision) next year. A Version in the
.NET framework consists of 4 integers for the major, minor, build number, and
revision in that format. When the build number uses the year as the first digit,
it becomes 3.0.70101.0 for example on January 1st of next year.
The build number only goes up to 65535. Oops. As an alternative, I think I'll
be sticking with the BuildDay method, using the [UpdateVersion tool](http://code.mattgriffith.net/UpdateVersion/). I was
hoping to be able to use the [AssemblyInfoTask](http://msbuildtasks.com/files/3/tasks/entry3.aspx) to
add a conditional task directly into my .csproj file, but maybe I can use some
form of [Exec task](http://msdn2.microsoft.com/en-us/library/x8zx72cd(en-US,VS.80).aspx) voodoo to get the UpdateVersion working with my build. I only want to
update the version number when I compile in release mode, so hopefully I can
write something with Condition=" '$(Configuration)' == 'release'" in the
BeforeCompile target.
