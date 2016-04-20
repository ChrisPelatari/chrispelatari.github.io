---
layout: post
title: Drag and Drop Urls in Windows Forms
---
<p>So I wanted to allow for this, right? What if I find something on the net 
that just begs me to post it, and I want to use the url as the source for my 
post? Well, it's insanely easy...but you still have to wire it up a little bit. 
From the article I found (using google, of course), I changed the source code to 
this:</p>
<p><pre style="COLOR: #000000"><br /><span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">1</span>		<font color="#0000ff">private</font> <font color="#0000ff">void</font> txtUrl_DragEnter(<font color="#0000ff">object</font> sender, System.Windows.Forms.DragEventArgs e) {
<br /><span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">2</span>			<font color="#0000ff">if</font>(e.Data.GetDataPresent(DataFormats.Text)){
<br /><span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">3</span>				e.Effect = DragDropEffects.All;
<br /><span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">4</span>			}
<br /><span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">5</span>		}
<br /><span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">6</span>
<br /><span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">7</span>		<font color="#0000ff">private</font> <font color="#0000ff">void</font> txtUrl_DragDrop(<font color="#0000ff">object</font> sender, System.Windows.Forms.DragEventArgs e) {
<br /><span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">8</span>			<font color="#0000ff">this</font>.txtUrl.Text = e.Data.GetData(DataFormats.Text).ToString();
<br /><span style="BORDER-RIGHT: #999999 1px solid; WIDTH: 40px; COLOR: #008284; MARGIN-RIGHT: 10px; BACKGROUND-COLOR: #e5e5e5; TEXT-ALIGN: right">9</span>		}</pre></p>
<p>where txtUrl is the url I want to use as a source for my post. Set AllowDrop 
= true in the designer, and you're good to go.</p>