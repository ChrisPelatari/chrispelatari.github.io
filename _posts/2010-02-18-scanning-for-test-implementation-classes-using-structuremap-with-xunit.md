---
layout: post
title: Scanning for Test implementation classes using StructureMap with xunit
date: 2010-02-18 07:59
author: chrispelatari
comments: true
categories: [Uncategorized]
---

<p>I have an <a href="http://xunit.codeplex.com/">xunit test project 
</a>that is using hand-rolled stubs as concrete implementations of interfaces. 
<a href="http://structuremap.sourceforge.net/Default.htm">StructureMap </a>is 
the DI container I'm using. I was looking at the names of my stubs, and they 
followed the convention of TestXYZ as the concrete implementation of IXYZ.</p>
<p>To use <a href="http://structuremap.sourceforge.net/Default.htm">StructureMap 
</a>from <a href="http://xunit.codeplex.com/">xunit tests</a>, I created a base 
class for any fact class that wanted to use ObjectFactory. In the base class 
ctor, I call the bootstrapper's ConfigureStructureMap method.</p>
<p>At first I just had a bunch of 
x.ForRequestedType&lt;IXYZ&gt;().TheDefaultIsConcreteType&lt;TestXYZ&gt;(); 
because I had only a handful of stubs and I didn't quite grasp how to scan like 
the default scanner, only adding "Test" to the beginning of the class name.</p>
<p>Then I found the <a href="http://www.bjoernrochel.de/2009/07/24/cutting-the-fluff-from-service-registration-or-how-to-do-funky-stuff-with-coc-castledynamicproxy-structuremap/">secret 
sauce over here</a>, via a method called FindPluginType.</p>
<p>Here is my bootstrapper code for my <a href="http://xunit.codeplex.com/">xunit test project</a>:</p><pre><span style="background-color:lightgrey;color:teal;">  1</span> <span style="color:blue;">public</span> <span style="color:blue;">class</span> TestScanner : ITypeScanner{
<span style="background-color:lightgrey;color:teal;">  2</span> 		<span style="color:blue;">public</span> <span style="color:blue;">void</span> Process(Type type, PluginGraph graph) {
<span style="background-color:lightgrey;color:teal;">  3</span> 			<span style="color:blue;">if</span>(type.Name.StartsWith(<span style="color:maroon;">"Test"</span>)){
<span style="background-color:lightgrey;color:teal;">  4</span> 				var pluginType = FindPluginType(type);
<span style="background-color:lightgrey;color:teal;">  5</span> 
<span style="background-color:lightgrey;color:teal;">  6</span> 				<span style="color:blue;">if</span>(pluginType == <span style="color:blue;">null</span>)
<span style="background-color:lightgrey;color:teal;">  7</span> 					<span style="color:blue;">return</span>;
<span style="background-color:lightgrey;color:teal;">  8</span> 
<span style="background-color:lightgrey;color:teal;">  9</span> 				graph.AddType(pluginType, type);
<span style="background-color:lightgrey;color:teal;"> 10</span> 			}				
<span style="background-color:lightgrey;color:teal;"> 11</span> 		}
<span style="background-color:lightgrey;color:teal;"> 12</span> 
<span style="background-color:lightgrey;color:teal;"> 13</span> 		<span style="color:blue;">static</span> Type FindPluginType(Type concreteType) {
<span style="background-color:lightgrey;color:teal;"> 14</span> 			var interfaceName = <span style="color:maroon;">"I"</span> + concreteType.Name.Replace(<span style="color:maroon;">"Test"</span>, <span style="color:maroon;">""</span>);
<span style="background-color:lightgrey;color:teal;"> 15</span> 
<span style="background-color:lightgrey;color:teal;"> 16</span> 			<span style="color:blue;">return</span> concreteType
<span style="background-color:lightgrey;color:teal;"> 17</span> 				.GetInterfaces()
<span style="background-color:lightgrey;color:teal;"> 18</span> 				.Where(t =&gt; <span style="color:blue;">string</span>.Equals(t.Name, interfaceName, StringComparison.Ordinal))
<span style="background-color:lightgrey;color:teal;"> 19</span> 				.FirstOrDefault();
<span style="background-color:lightgrey;color:teal;"> 20</span> 		}
<span style="background-color:lightgrey;color:teal;"> 21</span> 	}
<span style="background-color:lightgrey;color:teal;"> 22</span> 
<span style="background-color:lightgrey;color:teal;"> 23</span> 	<span style="color:blue;">public</span> <span style="color:blue;">static</span> <span style="color:blue;">class</span> Bootstrapper {
<span style="background-color:lightgrey;color:teal;"> 24</span> 		<span style="color:blue;">public</span> <span style="color:blue;">static</span> <span style="color:blue;">void</span> ConfigureStructureMap() {
<span style="background-color:lightgrey;color:teal;"> 25</span> 			ObjectFactory.Initialize(x =&gt;
<span style="background-color:lightgrey;color:teal;"> 26</span> 			{
<span style="background-color:lightgrey;color:teal;"> 27</span> 				x.Scan(s =&gt;
<span style="background-color:lightgrey;color:teal;"> 28</span> 				{
<span style="background-color:lightgrey;color:teal;"> 29</span> 					s.TheCallingAssembly();
<span style="background-color:lightgrey;color:teal;"> 30</span> 					s.WithDefaultConventions();
<span style="background-color:lightgrey;color:teal;"> 31</span> 					s.With&lt;TestScanner&gt;();
<span style="background-color:lightgrey;color:teal;"> 32</span> 				});
<span style="background-color:lightgrey;color:teal;"> 33</span> 			});
<span style="background-color:lightgrey;color:teal;"> 34</span> 		}
<span style="background-color:lightgrey;color:teal;"> 35</span> 	}</pre>What 
results is essentially the <a href="http://structuremap.sourceforge.net/ScanningAssemblies.htm#section9">DefaultConventionScanner</a>, 
only it's looking for TestXYZ as the concrete implementation of IXYZ. 
<p>Killer.</p>
