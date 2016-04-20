---
layout: post
title: skmMenu code change to work with xhtml doctypes
date: 2007-03-22 12:10
author: chrispelatari
comments: true
categories: [Uncategorized]
---

<p>This is just a re-statement of a <a href="http://www.gotdotnet.com/workspaces/messageboard/thread.aspx?id=a8ee64df-8f2a-483f-8594-10aaa66988ce&amp;threadid=48c4a040-054b-49f3-b40a-bc3fffa2ee97">forum 
thread</a> that discusses the fix, but since gotdotnet is not going to be 
around very much longer I thought I'd post this little tidbit here as well. 
Basically, when I upgraded one of my sites to .net 2.0, skmMenu got upgraded 
right along with it. The only issue was that all of my menus would show up at 
the far left corner of the screen, and when you try to navigate to them over 
there they disappear thanks to the menu items between the cursor and the target. 
I think I only saw this behavior in firefox, but the code fix works in both 
firefox and IE. I just went thru the .js file and the javascript in the .resx 
for embedded javascript goodness and placed a 'px' after any integer value. The 
reason for this is that firefox requires measurement properties be set with 
appropriate identifiers when it's displaying a structured document. Anyways, 
here's a reprint of the code:</p><pre><span style="color:blue;">function</span> skm_mousedOverMenu(menuID,elem,parent,displayedVertically,imageSource){
	skm_stopTick();
	skm_closeSubMenus(elem);
	<span style="color:blue;">var</span> childID=elem.id+<span style="color:maroon;">"-subMenu"</span>;  <span style="color:green;">// Display child menu if needed
</span>	<span style="color:blue;">if</span> (document.getElementById(childID)!=<span style="color:blue;">null</span>){  <span style="color:green;">// make the child menu visible and specify that its position is specified in absolute coordinates
</span>		document.getElementById(childID).style.display=<span style="color:maroon;">'block'</span>;
		document.getElementById(childID).style.position=<span style="color:maroon;">'absolute'</span>;
		skm_OpenMenuItems = skm_OpenMenuItems.concat(childID);
		<span style="color:blue;">if</span> (displayedVertically){ <span style="color:green;">// Set the child menu's left and top attributes according to the menu's offsets
</span>			document.getElementById(childID).style.left=skm_getAscendingLefts(parent)+parent.offsetWidth+<span style="color:maroon;">'px'</span>;
			document.getElementById(childID).style.top=skm_getAscendingTops(elem)+<span style="color:maroon;">'px'</span>;
			<span style="color:blue;">var</span> visibleWidth=parseInt(window.outerWidth?window.outerWidth-<span style="color:maroon;">9</span>:document.body.clientWidth,<span style="color:maroon;">10</span>+<span style="color:maroon;">'px'</span>);
			<span style="color:blue;">if</span> ((parseInt(document.getElementById(childID).offsetLeft,<span style="color:maroon;">10</span>+<span style="color:maroon;">'px'</span>)+parseInt(document.getElementById(childID).offsetWidth,<span style="color:maroon;">10</span>+<span style="color:maroon;">'px'</span>))&gt;visibleWidth) {
				document.getElementById(childID).style.left=visibleWidth-parseInt(document.getElementById(childID).offsetWidth,<span style="color:maroon;">10</span>+<span style="color:maroon;">'px'</span>);
			}
		}<span style="color:blue;">else</span>{  <span style="color:green;">// Set the child menu's left and top attributes according to the menu's offsets
</span>			document.getElementById(childID).style.left=skm_getAscendingLefts(elem)+<span style="color:maroon;">'px'</span>;
			document.getElementById(childID).style.top=skm_getAscendingTops(parent)+parent.offsetHeight+<span style="color:maroon;">'px'</span>;
			<span style="color:blue;">if</span> (document.getElementById(childID).offsetWidth&lt;elem.offsetWidth)
				document.getElementById(childID).style.width=elem.offsetWidth+<span style="color:maroon;">'px'</span>;
		}
	}
	<span style="color:blue;">if</span> (skm_SelectedMenuStyleInfos[menuID] != <span style="color:blue;">null</span>) skm_SelectedMenuStyleInfos[menuID].applyToElement(elem);
	<span style="color:blue;">if</span> (skm_highlightTopMenus[menuID]){
		<span style="color:blue;">var</span> eId=elem.id+<span style="color:maroon;">''</span>;
		<span style="color:blue;">while</span> (eId.indexOf(<span style="color:maroon;">'-subMenu'</span>)&gt;=<span style="color:maroon;">0</span>){
			eId=eId.substring(<span style="color:maroon;">0</span>, eId.lastIndexOf(<span style="color:maroon;">'-subMenu'</span>));
			skm_SelectedMenuStyleInfos[menuID].applyToElement(document.getElementById(eId));
		}
	}	
	<span style="color:blue;">if</span> (imageSource!=<span style="color:maroon;">''</span>){
		setimage(elem,imageSource)
	}
}</pre><pre><span style="color:blue;">function</span> skm_shimSetVisibility(makevisible, tableid){
	<span style="color:blue;">var</span> tblRef=document.getElementById(tableid);
	<span style="color:blue;">var</span> IfrRef=document.getElementById(<span style="color:maroon;">'shim'</span>+tableid);
	<span style="color:blue;">if</span> (tblRef!=<span style="color:blue;">null</span> &amp;&amp; IfrRef!=<span style="color:blue;">null</span>){
		<span style="color:blue;">if</span>(makevisible){
			IfrRef.style.width=tblRef.offsetWidth+<span style="color:maroon;">'px'</span>;
			IfrRef.style.height=tblRef.offsetHeight+<span style="color:maroon;">'px'</span>;
			IfrRef.style.top=tblRef.style.top+<span style="color:maroon;">'px'</span>;
			IfrRef.style.left=tblRef.style.left+<span style="color:maroon;">'px'</span>;
			IfrRef.style.zIndex=tblRef.style.zIndex-<span style="color:maroon;">1</span>;
			IfrRef.style.display=<span style="color:maroon;">"block"</span>;
		}<span style="color:blue;">else</span>{
			IfrRef.style.display=<span style="color:maroon;">"none"</span>;
		}
	}
}</pre>
<p>These were the only two functions that needed code adjustment. Enjoy.</p>
<p class="media">[ Currently Playing : Mannequin Republic - At the Drive-In - 
Relationship of Command [Japan (3:02) ]</p>
