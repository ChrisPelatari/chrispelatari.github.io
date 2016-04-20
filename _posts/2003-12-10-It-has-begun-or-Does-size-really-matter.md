---
layout: post
title: It has begun or Does size really matter?
---
<p>I finally decided on a name for my project - PostModern. I had already gotten 
syntax highlighting worked out, but I ended up using a different component than 
I had originally planned. I'm using a component from <a href="http://www.squishyweb.com" target="_blank">SquishyWare</a> called <a href="http://www.squishyweb.com/ware/products.asp?q=squishysyntax" target="_blank">squishySyntaxHighlighter</a>. It's really nice...simple, easy to 
modify, and it looks pretty spiffy too.</p>
<p>So here's the thing. It creates a little bit of markup by using [span style=] 
tags where you would expect coloration, so if you're posting any sizeable amount 
of code, it can get bloated. (<em>That's</em> why I put the second part of the 
title in there, you nasty nelly you!)</p>
<p>I've found that it's a little bit difficult, if possible at all, to grab the 
selected text in the HtmlComponent that I'll probably be using, so a 
drawback of syntax highlighting is that you'll more than likely have to do it 
from the [html] tab that we're all so familiar with. Also, I've found that the 
HtmlComponent (and others too, so it must be a mshtml thing) will colorize text 
pasted from Visual Studio. Here's the difference:</p>

<p>[pasted directly into the design surface]<br /><font color="#0000ff">using</font> 
System;</p>
<p><font color="#0000ff">namespace</font> HighlightTest</p>
<p>{</p>
<p><font color="#808080">///</font><font color="#008000"> </font><font color="#808080"><summary></summary></font></p>
<p><font color="#808080">///</font><font color="#008000"> Summary description for 
SampleCs.</font></p>
<p><font color="#808080">///</font><font color="#008000"> </font><font color="#808080"></font></p>
<p><font color="#0000ff">public</font> <font color="#0000ff">class</font> 
SampleCs</p>
<p>{</p>
<p><font color="#0000ff">public</font> SampleCs()</p>
<p>{</p>
<p><font color="#008000">//</font></p>
<p><font color="#008000">// TODO: Add constructor logic here</font></p>
<p><font color="#008000">//</font></p>
<p>}</p>
<p><font color="#0000ff">public</font> <font color="#0000ff">void</font> 
DoSomething( <font color="#0000ff">string</font> s ) {</p>
<p><font color="#0000ff">if</font>( s == "string literal" ) {</p>
<p><font color="#0000ff">return</font>;</p>
<p>}</p>
<p>}</p>
<p><font color="#0000ff">#region</font> This is a Region</p>
<p><font color="#0000ff">private</font> <font color="#0000ff">void</font> 
DoSomethingElse( <font color="#0000ff">int</font> i ) {</p>
<p><font color="#0000ff">int</font> x = i;</p>
<p>}</p>
<p><font color="#0000ff">#endregion</font></p>
<p>}</p>
<p>}</p>
<p> [using the SyntaxHighlighter]<br /></p>
<pre><span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">1</span><span style="COLOR: #0000ff">using</span> System;
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">2</span>
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">3</span><span style="COLOR: #0000ff">namespace</span> HighlightTest
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">4</span>{
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">5</span>	<span style="COLOR: #848284">///</span><span style="COLOR: #008200"> <span style="COLOR: #848284"><summary></summary></span></span>
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">6</span>	<span style="COLOR: #848284">///</span><span style="COLOR: #008200"> Summary description for SampleCs.</span>
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">7</span>	<span style="COLOR: #848284">///</span><span style="COLOR: #008200"> <span style="COLOR: #848284"></span></span>
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">8</span>	<span style="COLOR: #0000ff">public</span> <span style="COLOR: #0000ff">class</span> SampleCs
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">9</span>	{
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">10</span>		<span style="COLOR: #0000ff">public</span> SampleCs()
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">11</span>		{
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">12</span>			<span style="COLOR: #008200">//</span>
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">13</span>			<span style="COLOR: #008200">// TODO: Add constructor logic here</span>
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">14</span>			<span style="COLOR: #008200">//</span>
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">15</span>		}
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">16</span>
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">17</span>		<span style="COLOR: #0000ff">public</span> <span style="COLOR: #0000ff">void</span> DoSomething( <span style="COLOR: #0000ff">string</span> s ) {
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">18</span>			<span style="COLOR: #0000ff">if</span>( s == <span style="COLOR: #848284">"string literal"</span> ) {
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">19</span>				<span style="COLOR: #0000ff">return</span>;
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">20</span>			}
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">21</span>		}
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">22</span><span style="COLOR: #6699cc">
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">23</span>		#region This is a Region</span><span id="region1" style="DISPLAY: inline">
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">24</span>		
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">25</span>		<span style="COLOR: #0000ff">private</span> <span style="COLOR: #0000ff">void</span> DoSomethingElse( <span style="COLOR: #0000ff">int</span> i ) {
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">26</span>			<span style="COLOR: #0000ff">int</span> x = i;
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">27</span>		}
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">28</span></span><span style="COLOR: #6699cc">		#endregion</span>
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">29</span>	}
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">30</span>}
<span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">31</span></pre>
<p>So there's a little bit more work to go thru, but the end result is that it's 
already formatted the way I like. What do you think about 
that?</p>