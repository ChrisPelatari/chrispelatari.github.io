---
layout: post
title: Set your FileAccess!
---
When I was working on the latest release of the <a href="http://PostXING.url123.com/plugin1.0.5004.1">BlogThisUsingPostXINGPlugin</a>, 
I kept running into file access issues.

The whole thing was an excersize in refactoring - well, really, the whole 
thing WAS a refactor, since the basic functionality already existed, but I was 
making additions in how things were going to work.

First, I changed the XsltStream to return a FileStream or a 
ManifestResourceStream, based on the existence of a user-specific file:

<pre><span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  1</span> 		Stream XsltStream
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  2</span> 		{
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  3</span> 			<span style="COLOR: blue">get</span>
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  4</span> 			{
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  5</span> 				<span style="COLOR: blue">string</span> filePath = Path.Combine(ConfigurationPath, <span style="COLOR: blue">this</span>.BlogType.ToString() + <span style="COLOR: maroon">".xslt"</span>);
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  6</span> 				<span style="COLOR: blue">if</span>(File.Exists(filePath)){
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  7</span> 					<span style="COLOR: green">//read from a file stream.
</span><span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  8</span> 					FileStream fs = <span style="COLOR: blue">new</span> FileStream(filePath, FileMode.Open);
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  9</span> 					<span style="COLOR: blue">return</span> (Stream)fs;
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 10</span> 				}<span style="COLOR: blue">else</span>{
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 11</span> 					<span style="COLOR: blue">string</span> resourceName = <span style="COLOR: maroon">"PostXING.Rss.BlogExtensions.Resources."</span> + <span style="COLOR: blue">this</span>.BlogType.ToString() + <span style="COLOR: maroon">".xslt"</span>;
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 12</span> 					<span style="COLOR: blue">return</span> Assembly.GetExecutingAssembly().GetManifestResourceStream(resourceName);
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 13</span> 				}
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 14</span> 			}
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 15</span> 		}</pre>

Again, this part was shamelessly <strike>lifted </strike> modified from 
<a href="http://haacked.com">haacked</a> who generously gave out the source 
code for his BlogThisUsingWbloggarPlugin. (the configurationPath property was 
changed a bit to enable more than one file to go into that particular path).

Then I added a button next to each option in the config dialog that says 
simply "Customize...". Pressing this button opens a modal form that loads up the 
text from the user-defined file if it exists, else from the resource 
stream.:

<pre><span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  1</span> 		<span style="COLOR: blue">string</span> transformPath;
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  2</span> 
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  3</span> 		<span style="COLOR: blue">public</span> CustomizeForm()
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  4</span> 		{
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  5</span> 			<span style="COLOR: green">//
</span><span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  6</span> 			<span style="COLOR: green">// Required for Windows Form Designer support
</span><span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  7</span> 			<span style="COLOR: green">//
</span><span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  8</span> 			InitializeComponent();
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  9</span> 
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 10</span> 		}
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 11</span> 
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 12</span> 		<span style="COLOR: blue">public</span> CustomizeForm(<span style="COLOR: blue">string</span> TransformToCustomize) : <span style="COLOR: blue">this</span>(){
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 13</span> 			transformPath = Path.Combine(BlogThisUsingPostXINGPlugin.ConfigurationPath, <span style="COLOR: blue">string</span>.Format(<span style="COLOR: maroon">"{0}.xslt"</span>, TransformToCustomize));
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 14</span> 
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 15</span> 			<span style="COLOR: blue">this</span>.LoadTransform(TransformToCustomize);
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 16</span> 		}	
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 17</span> 
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 18</span> 		<span style="COLOR: blue">private</span> <span style="COLOR: blue">void</span> LoadTransform(<span style="COLOR: blue">string</span> TransformToCustomize){			
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 19</span> 			<span style="COLOR: blue">string</span> resourceName = <span style="COLOR: blue">string</span>.Format(<span style="COLOR: maroon">"PostXING.Rss.BlogExtensions.Resources.{0}.xslt"</span>, TransformToCustomize);
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 20</span> 			<span style="COLOR: green">//Stream resourceStream;
</span><span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 21</span> 			StreamReader sr;
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 22</span> 
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 23</span> 			<span style="COLOR: blue">if</span>(File.Exists(transformPath)){
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 24</span> 				sr = <span style="COLOR: blue">new</span> StreamReader(transformPath);
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 25</span> 				<span style="COLOR: blue">this</span>.rtbTransform.Text = sr.ReadToEnd();
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 26</span> 				sr.Close();
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 27</span> 				
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 28</span> 			}<span style="COLOR: blue">else</span>{
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 29</span> 				sr = <span style="COLOR: blue">new</span> StreamReader(ResourceStream(resourceName));
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 30</span> 				<span style="COLOR: blue">this</span>.rtbTransform.Text = sr.ReadToEnd();
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 31</span> 				sr.Close();
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 32</span> 				
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 33</span> 			}
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 34</span> 		}
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 35</span> 
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 36</span> 		Stream ResourceStream(<span style="COLOR: blue">string</span> resourceName){
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 37</span> 			<span style="COLOR: blue">return</span> Assembly.GetExecutingAssembly().GetManifestResourceStream(resourceName);
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 38</span> 		}</pre>

3 buttons were added to the form: Revert to Original, Apply, and Cancel. I 
didn't really think that I needed DialogResults, since you have to invoke the 
plugin via its menu every time you want to use it. Revert to Original just 
deletes the user-defined file. Cancel simply closes the form and does nothing. 
Apply does this:

<pre><span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  1</span> 		<span style="COLOR: blue">private</span> <span style="COLOR: blue">void</span> btnApply_Click(<span style="COLOR: blue">object</span> sender, System.EventArgs e) {
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  2</span> 			<span style="COLOR: blue">if</span>(File.Exists(transformPath)){
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  3</span> 				File.Delete(transformPath);
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  4</span> 			}
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  5</span> 
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  6</span> 			StreamWriter sw = <span style="COLOR: blue">new</span> StreamWriter(transformPath, <span style="COLOR: maroon">false</span>); <span style="COLOR: green">//doesn't release file handle?
</span><span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  7</span> 			sw.Write(<span style="COLOR: blue">this</span>.rtbTransform.Text);
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  8</span> 			sw.Flush();
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  9</span> 			sw.Close();
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 10</span> 
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 11</span> 			<span style="COLOR: blue">this</span>.Close();
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 12</span> 		}</pre>

Notice my little note to myself? It turned out that I tried using the using 
statement, using File.CreateText(transformPath) (which is why the pre-step 
File.Delete is in there) and I kept getting "Cannot access file 'blah' because 
it is in use by another process." When I opened up sysinternal's process 
explorer and searched for the file, it said that the file handle was opened by 
RssBandit. grr.

All I ended up having to do was to add one argument to File.Open from the 
XsltStream property getter:

<pre><span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  1</span> 		Stream XsltStream
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  2</span> 		{
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  3</span> 			<span style="COLOR: blue">get</span>
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  4</span> 			{
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  5</span> 				<span style="COLOR: blue">string</span> filePath = Path.Combine(ConfigurationPath, <span style="COLOR: blue">this</span>.BlogType.ToString() + <span style="COLOR: maroon">".xslt"</span>);
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  6</span> 				<span style="COLOR: blue">if</span>(File.Exists(filePath)){
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  7</span> 					<span style="COLOR: green">//read from a file stream.
</span><span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  8</span> 					FileStream fs = <span style="COLOR: blue">new</span> FileStream(filePath, FileMode.Open, FileAccess.Read);
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  9</span> 					<span style="COLOR: blue">return</span> (Stream)fs;
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 10</span> 				}<span style="COLOR: blue">else</span>{
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 11</span> 					<span style="COLOR: blue">string</span> resourceName = <span style="COLOR: maroon">"PostXING.Rss.BlogExtensions.Resources."</span> + <span style="COLOR: blue">this</span>.BlogType.ToString() + <span style="COLOR: maroon">".xslt"</span>;
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 12</span> 					<span style="COLOR: blue">return</span> Assembly.GetExecutingAssembly().GetManifestResourceStream(resourceName);
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 13</span> 				}
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 14</span> 			}
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 15</span> 		}</pre>

And bam! the problem went away. It looks like the default for a new 
FileStream (sans FileAccess attribute) is FileAccess.ReadWrite. Anyways, I hope 
this helps someone else out there from banging their head too much.

<p class="media">[ Currently Playing : Inertiatic ESP - Mars Volta - De-Loused In 
The Comatorium (4:23) ]</p>