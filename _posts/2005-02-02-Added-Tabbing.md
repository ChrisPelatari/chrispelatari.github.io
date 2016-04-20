---
layout: post
---
I recently added Tabbing functionality for 
indenting/outdenting (hey, it's a trident term :) in my dogfood version of 
PostXING.

> Quoting has just become 100 times easier for me.

I prefer to use the keyboard when 
posting/changing text attributes when possible, and this whole no tabbing 
business finally got me a little fed up. Wanna know the funny part? It ended up 
being about 8 lines of code, give or take for whitespace:

<pre><span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  1</span> <span style="COLOR: blue">protected</span> <span style="COLOR: blue">override</span> <span style="COLOR: blue">bool</span> ProcessCmdKey(<span style="COLOR: blue">ref</span> Message msg, Keys keyData) {
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  2</span> 	<span style="COLOR: blue">if</span>(keyData == Keys.Tab){
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  3</span> 		<span style="COLOR: blue">this</span>._designEditor.TextFormatting.Indent();
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  4</span> 	}<span style="COLOR: blue">else</span> <span style="COLOR: blue">if</span>(keyData == (Keys.Tab | Keys.Shift)){
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  5</span> 		<span style="COLOR: blue">this</span>._designEditor.TextFormatting.Unindent();
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  6</span> 	}
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  7</span> 			
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  8</span> 	<span style="COLOR: blue">return</span> <span style="COLOR: blue">base</span>.ProcessCmdKey (<span style="COLOR: blue">ref</span> msg, keyData);
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  9</span> }</pre>

What other unsupported keyboard shortcuts 
would you like to see in PostXING (get em while I've got it fresh on my mind 
:)

<p class="media">[ Currently Playing : Dazed And Confused - Led Zeppelin - BBC 
Sessions CD 2 (18:36) ]</p>