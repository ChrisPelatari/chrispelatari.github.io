---
layout: post
title: SubSonic Scaffold control - a GridView with Class
date: 2007-03-08 15:40
author: chrispelatari
comments: true
categories: [aspnet,SubSonic]
---

So I've been able to dig my teeth into some asp.net hacking recently, and
I've been ~~wrestling with~~ learning to use [SubSonic](http://codeplex.com/actionpack") in the process.

In dealing with the scaffold control I ran into a funny issue: none of the
exposed properties on the scaffold control will output any style info of the
GridView that the control uses (that I could figure out anyways). I ended up
with black text on a black background. :/ Seeing as I have the source, I decided
to give the scaffold control's GridView a little class...hello GridViewCssClass
property! I set it up just like the EditTable*CssClass properties, just a string
property, with similar attributes to the other properties hanging around
there:

```csharp
[Bindable(true)]
[Category("Display")]
[Description("Sets the CSS class used by the gridview.")]
[DefaultValue(ScaffoldCSS.WRAPPER)]
//CDF: just to have something to start with.
public string GridViewCssClass {
	get { return _gridViewCssClass; }
	set { _gridViewCssClass = value; }
}
```

Then, in the CreateGrid method make it actually do something:

```csharp
private void CreateGrid()	{
			Label lblTitle = new Label();
      surroundingPanel.Controls.Add(lblTitle);
      lblTitle.Text = "&lt;h2&gt;" + schema.Name + " Admin&lt;/h2&gt;";

      grid.ID = "grid";
	    grid.CssClass = this.GridViewCssClass;

      surroundingPanel.Controls.Add(grid);

      if (!Page.IsPostBack) {
      	BindGrid(String.Empty);
      }

			//add a column to the grid for editing
}
```

And now I can declaratively set the CssClass that the GridView uses to, oh,
say, .whitetext :)
