---
layout: post
title: SubSonic Scaffold control - a GridView with Class
date: 2007-03-08 15:40
author: chrispelatari
comments: true
categories: [Uncategorized]
---

<p>So I've been able to dig my teeth into some asp.net hacking recently, and 
I've been <strike>wrestling with</strike> learning to use <a href="http://codeplex.com/actionpack">SubSonic </a>in the process.</p>
<p>In dealing with the scaffold control I ran into a funny issue: none of the 
exposed properties on the scaffold control will output any style info of the 
GridView that the control uses (that I could figure out anyways). I ended up 
with black text on a black background. :/ Seeing as I have the source, I decided 
to give the scaffold control's GridView a little class...hello GridViewCssClass 
property! I set it up just like the EditTable*CssClass properties, just a string 
property, with similar attributes to the other properties hanging around 
there:</p><pre>[Bindable(<span style="color:maroon;">true</span>)]
[Category(<span style="color:maroon;">"Display"</span>)]
[Description(<span style="color:maroon;">"Sets the CSS class used by the gridview."</span>)]
[DefaultValue(ScaffoldCSS.WRAPPER)] <span style="color:green;">//CDF: just to have something to start with.
</span><span style="color:blue;">public</span> <span style="color:blue;">string</span> GridViewCssClass {
	<span style="color:blue;">get</span> { <span style="color:blue;">return</span> _gridViewCssClass; }
	<span style="color:blue;">set</span> { _gridViewCssClass = value; }
}</pre>
<p>Then, in the CreateGrid method make it actually do something:</p><pre>        <span style="color:blue;">private</span> <span style="color:blue;">void</span> CreateGrid()
        {
            Label lblTitle = <span style="color:blue;">new</span> Label();
            surroundingPanel.Controls.Add(lblTitle);
            lblTitle.Text = <span style="color:maroon;">"&lt;h2&gt;"</span> + schema.Name + <span style="color:maroon;">" Admin&lt;/h2&gt;"</span>;

            grid.ID = <span style="color:maroon;">"grid"</span>;
	    <strong>grid.CssClass = <span style="color:blue;">this</span>.GridViewCssClass;</strong>

            surroundingPanel.Controls.Add(grid);

            <span style="color:blue;">if</span> (!Page.IsPostBack)
            {
                BindGrid(String.Empty);
            }
            <span style="color:green;">//add a column to the grid for editing
</span>        }</pre>
<p>And now I can declaratively set the CssClass that the GridView uses to, oh, 
say, .whitetext :)</p>
