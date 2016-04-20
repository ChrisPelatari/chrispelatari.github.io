---
layout: post
title: CODESNIP - Creating C# like indexers in VB.NET
---
Well, kind of :) I have a collection that I want to access in C# with an 
indexer, the only problem is that the collection is written in VB.NET as part of 
a library which I need to consume and would be foolhardy to try and rewrite in 
C#.

It's just a mixture of attributes and keywords - but gets me from having 
to call 

<pre>MyCollection.get_Item(<font color="#004884">"key"</font>);</pre>

to

<pre>MyCollection[<font color="#004884">"key"</font>];</pre>
Just a stylistic approach on my end to keep the readability of my C# consumer 
as high as possible. This is basically what I used:

<pre><font color="#0000ff">Imports</font> System.Reflection
...
&lt;DefaultMember(<font color="#004884">"Item"</font>)&gt; _ 
<font color="#0000ff">Public</font> <font color="#0000ff">Class</font> MyCollection
	<font color="#0000ff">Inherits</font> System.Collections.CollectionBase

	<font color="#0000ff">Public</font> <font color="#0000ff">Sub</font> Add(<font color="#0000ff">ByVal</font> NewObj <font color="#0000ff">As</font> <font color="#0000ff">MyClass</font>)
		List.Add(NewObj)
	<font color="#0000ff">End</font> <font color="#0000ff">Sub</font>

	...

	<font color="#0000ff">Default</font> <font color="#0000ff">Public</font> <font color="#0000ff">Overloads</font> <font color="#0000ff">ReadOnly</font> <font color="#0000ff">Property</font> Item(<font color="#0000ff">ByVal</font> Index <font color="#0000ff">As</font> Int32) _
		<font color="#0000ff">As</font> <font color="#0000ff">MyClass</font>
		<font color="#0000ff">Get</font>
			<font color="#0000ff">Return</font>(<font color="#0000ff">CType</font>(List.Item(Index), <font color="#0000ff">MyClass</font>)
		<font color="#0000ff">End</font> <font color="#0000ff">Get</font>
	<font color="#0000ff">End</font> <font color="#0000ff">Property</font>

	<font color="#0000ff">Default</font> <font color="#0000ff">Public</font> <font color="#0000ff">Overloads</font> <font color="#0000ff">ReadOnly</font> <font color="#0000ff">Property</font> Item(<font color="#0000ff">ByVal</font> Key <font color="#0000ff">As</font> <font color="#0000ff">String</font>) _
		<font color="#0000ff">As</font> <font color="#0000ff">MyClass</font>
		<font color="#0000ff">Get</font>
			<font color="#0000ff">Return</font>(GetByKey(Key))
		<font color="#0000ff">End</font> <font color="#0000ff">Get</font>
	<font color="#0000ff">End</font> <font color="#0000ff">Property</font>
...
<font color="#0000ff">End</font> <font color="#0000ff">Class</font></pre>
I don't know if the Default on the properties are required, but this worked 
for me. So I'm not messing with it :) Hope this can help someone else out 
there.

\[ Currently Playing : High and Dry - Radiohead - The Bends 
(4:05) \]