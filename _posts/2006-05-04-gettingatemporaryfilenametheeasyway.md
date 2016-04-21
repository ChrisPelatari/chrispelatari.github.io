---
layout: post
title: Getting a temporary filename the easy way
date: 2006-05-04 15:02
author: chrispelatari
comments: true
categories: [csharp]
---

If you need to generate temporary / semi-unique filenames, here is a little
snippet that uses the framework:

```csharp
using System.IO;

string GetTempFileName(){
	return Path.GetFileNameWithoutExtension(Path.GetTempFileName());
}
```

As the name implies, this will return the temporary name of a file without
the extension, so it's up to you to add whatever filetype you may be trying to
create. For example, let's say I wanted to generate a .gif:

```csharp
string GetTempGifFileName(){
	return string.Format("{0}.{1}", GetTempFileName(), "gif");
}
```

I had overlooked this little piece of functionality because the component
that I was using generated filenames with GUIDs, so I never really worried about
it. Way to make my life easier, .netfx :)

[ Currently Playing : Mississippi Queen - Ozzy Osbourne - Under
Cover (4:11) ]
