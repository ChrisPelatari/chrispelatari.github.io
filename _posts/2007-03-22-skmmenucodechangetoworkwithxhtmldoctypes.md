---
layout: post
title: skmMenu code change to work with xhtml doctypes
date: 2007-03-22 12:10
author: chrispelatari
comments: true
categories: [aspnet, javascript]
---

This is just a re-statement of a [forum
thread](http://www.gotdotnet.com/workspaces/messageboard/thread.aspx?id=a8ee64df-8f2a-483f-8594-10aaa66988ce&amp;threadid=48c4a040-054b-49f3-b40a-bc3fffa2ee97) that discusses the fix, but since gotdotnet is not going to be
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
here's a reprint of the code:

```javascript
function skm_mousedOverMenu(menuID,elem,parent,displayedVertically,imageSource){
	skm_stopTick();
	skm_closeSubMenus(elem);

	var childID = elem.id + "-subMenu";  

	// Display child menu if needed
  if (document.getElementById(childID) != null){  
		// make the child menu visible and specify that its position is specified in absolute coordinates
		document.getElementById(childID).style.display = 'block';
		document.getElementById(childID).style.position = 'absolute';
		skm_OpenMenuItems = skm_OpenMenuItems.concat(childID);

		if (displayedVertically){
			// Set the child menu's left and top attributes according to the menu's offsets
			document.getElementById(childID).style.left = skm_getAscendingLefts(parent) + parent.offsetWidth + 'px';
			document.getElementById(childID).style.top = skm_getAscendingTops(elem) + 'px';

			var visibleWidth = parseInt(window.outerWidth ? window.outerWidth - 9 : document.body.clientWidth, 10 + 'px');

			if ((parseInt(document.getElementById(childID).offsetLeft,10 + 'px') + parseInt(document.getElementById(childID).offsetWidth, 10 + 'px')) > visibleWidth) {
				document.getElementById(childID).style.left = visibleWidth - parseInt(document.getElementById(childID).offsetWidth, 10 + 'px');
			}
		}else{  
			// Set the child menu's left and top attributes according to the menu's offsets
			document.getElementById(childID).style.left = skm_getAscendingLefts(elem) + 'px';
			document.getElementById(childID).style.top = skm_getAscendingTops(parent) + parent.offsetHeight + 'px';

			if (document.getElementById(childID).offsetWidth < elem.offsetWidth)
				document.getElementById(childID).style.width = elem.offsetWidth + 'px';
		}
	}

	if (skm_SelectedMenuStyleInfos[menuID] != null) skm_SelectedMenuStyleInfos[menuID].applyToElement(elem);
	if (skm_highlightTopMenus[menuID]){
		var eId=elem.id + ' ';
		while (eId.indexOf('-subMenu') >= 0){
			eId=eId.substring(0, eId.lastIndexOf('-subMenu'));
			skm_SelectedMenuStyleInfos[menuID].applyToElement(document.getElementById(eId));
		}
	}

	if (imageSource != ''){
		setimage(elem,imageSource)
	}
}

function skm_shimSetVisibility(makevisible, tableid){
	var tblRef = document.getElementById(tableid);
	var IfrRef = document.getElementById('shim' + tableid);

	if (tblRef != null && IfrRef != null){
		if(makevisible){
			IfrRef.style.width = tblRef.offsetWidth + 'px';
			IfrRef.style.height = tblRef.offsetHeight + 'px';
			IfrRef.style.top = tblRef.style.top + 'px';
			IfrRef.style.left = tblRef.style.left + 'px';
			IfrRef.style.zIndex = tblRef.style.zIndex - 1;
			IfrRef.style.display = "block";
		}else{
			IfrRef.style.display = "none";
		}
	}
}
```

These were the only two functions that needed code adjustment. Enjoy.

[ Currently Playing : Mannequin Republic - At the Drive-In -
Relationship of Command [Japan (3:02) ]
