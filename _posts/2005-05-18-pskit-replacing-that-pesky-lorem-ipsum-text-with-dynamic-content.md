---
layout: post
title: "PSKit: Replacing that pesky Lorem Ipsum text with dynamic content"
---
 
The Personal Website Starter Kit is a great resource for getting up and 
running with asp.net 2.0 beta. I've been using it to check out some features 
while waiting for other projects to get to a point where I feel like I can 
contribute more than just criticism (sorry y'all :) That said, the default.aspx 
page comes with a FormsView that rotates pictures from your PSKit albums, but 
everything else is static content! That is, you're greeted on the front page 
with something like:

<blockquote dir="ltr" style="MARGIN-RIGHT: 0px">
  <h3>Welcome to my Website!</h3>
  <p>On this site you will find lorem ipsum dolor sit amet...</p></blockquote>

Earlier, I had tried using one of the new data controls in asp.net - 
namely the FormView. I ran into a few issues with this control, mostly having to 
do with having to know what ID I was using in the database to set or edit the 
FormView's contents - I'm sure I could have worked out a way to set the ID to 
use in some clever way, but then I looked at the actual content that comes stock 
with the PSKit and it hit me...

A DataList.

It's already separated by a horizontal rule - all I really need is to 
bind a good old DataList to a couple of database entries and I've got something 
that I can update, oh, say twice a year or whatever. heh.

I used a similar table structure to the one from before:

<blockquote dir="ltr" style="MARGIN-RIGHT: 0px">
  <p dir="ltr"><u>Content<br /></u>ContentID<br />Heading<br />Content<br />IsVisible</p></blockquote>

I had to actually write code (gasp!) to get it working the way I 
wanted it to, but it was pretty stock stuff thankfully. I just set up a 
SqlDataSource pointing to this table's CRUD procedures:

<pre>                
	<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">asp:SqlDataSource</span> <span style="COLOR: red">ID</span>="<span style="COLOR: dodgerblue">SqlDataSource1</span>" <br />                  <span style="COLOR: red">runat</span>="<span style="COLOR: dodgerblue">server</span>" <br />                  <span style="COLOR: red">ConnectionString</span>="<font style="BACKGROUND-COLOR: yellow" color="black">&lt;</font><span style="COLOR: dodgerblue"><font style="BACKGROUND-COLOR: yellow" color="black">%</font>$ ConnectionStrings:Personal <font style="BACKGROUND-COLOR: yellow" color="black">%&gt;</font></span>" <br />                  <span style="COLOR: red">ProviderName</span>="<span style="COLOR: dodgerblue">System.Data.SqlClient</span>"
                  <span style="COLOR: red">SelectCommand</span>="<span style="COLOR: dodgerblue">GetContents</span>" <br />                  <span style="COLOR: red">SelectCommandType</span>="<span style="COLOR: dodgerblue">StoredProcedure</span>" <br />                  <span style="COLOR: red">DeleteCommand</span>="<span style="COLOR: dodgerblue">RemoveContent</span>" <br />                  <span style="COLOR: red">DeleteCommandType</span>="<span style="COLOR: dodgerblue">StoredProcedure</span>"<br />                  <span style="COLOR: red">InsertCommand</span>="<span style="COLOR: dodgerblue">AddContent</span>" <br />                  <span style="COLOR: red">InsertCommandType</span>="<span style="COLOR: dodgerblue">StoredProcedure</span>"<br />                  <span style="COLOR: red">UpdateCommand</span>="<span style="COLOR: dodgerblue">EditContent</span>"   <br />                  <span style="COLOR: red">UpdateCommandType</span>="<span style="COLOR: dodgerblue">StoredProcedure</span>"<span style="COLOR: blue">&gt;</span>
		  <span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">DeleteParameters</span><span style="COLOR: blue">&gt;</span>
		    <span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">asp:Parameter</span> <span style="COLOR: red">Name</span>="<span style="COLOR: dodgerblue">Content_ID</span>" <span style="COLOR: red">Type</span>="<span style="COLOR: dodgerblue">Int32</span>" /<span style="COLOR: blue">&gt;</span>
		  <span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">DeleteParameters</span><span style="COLOR: blue">&gt;</span>
		  <span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">UpdateParameters</span><span style="COLOR: blue">&gt;</span>
		    <span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">asp:Parameter</span> <span style="COLOR: red">Name</span>="<span style="COLOR: dodgerblue">Content_ID</span>" <span style="COLOR: red">Type</span>="<span style="COLOR: dodgerblue">Int32</span>" /<span style="COLOR: blue">&gt;</span>
		    <span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">asp:Parameter</span> <span style="COLOR: red">Name</span>="<span style="COLOR: dodgerblue">Heading</span>" <span style="COLOR: red">Type</span>="<span style="COLOR: dodgerblue">String</span>" /<span style="COLOR: blue">&gt;</span>
		    <span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">asp:Parameter</span> <span style="COLOR: red">Name</span>="<span style="COLOR: dodgerblue">Content</span>" <span style="COLOR: red">Type</span>="<span style="COLOR: dodgerblue">String</span>" /<span style="COLOR: blue">&gt;</span>
		    <span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">asp:Parameter</span> <span style="COLOR: red">Name</span>="<span style="COLOR: dodgerblue">IsVisible</span>" <span style="COLOR: red">Type</span>="<span style="COLOR: dodgerblue">Boolean</span>" /<span style="COLOR: blue">&gt;</span>
		  <span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">UpdateParameters</span><span style="COLOR: blue">&gt;</span>
		  <span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">InsertParameters</span><span style="COLOR: blue">&gt;</span>
		    <span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">asp:Parameter</span> <span style="COLOR: red">Direction</span>="<span style="COLOR: dodgerblue">InputOutput</span>" <span style="COLOR: red">Name</span>="<span style="COLOR: dodgerblue">Content_ID</span>" <span style="COLOR: red">Type</span>="<span style="COLOR: dodgerblue">Int32</span>" /<span style="COLOR: blue">&gt;</span>
		    <span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">asp:Parameter</span> <span style="COLOR: red">Name</span>="<span style="COLOR: dodgerblue">Heading</span>" <span style="COLOR: red">Type</span>="<span style="COLOR: dodgerblue">String</span>" /<span style="COLOR: blue">&gt;</span>
		    <span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">asp:Parameter</span> <span style="COLOR: red">Name</span>="<span style="COLOR: dodgerblue">Content</span>" <span style="COLOR: red">Type</span>="<span style="COLOR: dodgerblue">String</span>" /<span style="COLOR: blue">&gt;</span>
		    <span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">asp:Parameter</span> <span style="COLOR: red">Name</span>="<span style="COLOR: dodgerblue">IsVisible</span>" <span style="COLOR: red">Type</span>="<span style="COLOR: dodgerblue">Boolean</span>" /<span style="COLOR: blue">&gt;</span>
		  <span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">InsertParameters</span><span style="COLOR: blue">&gt;</span>
                <span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">asp:SqlDataSource</span><span style="COLOR: blue">&gt;</span></pre>

Then the DataList itself:

<pre>			<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">asp:DataList</span> <span style="COLOR: red">ID</span>="<span style="COLOR: dodgerblue">DataList1</span>" <br /><span style="COLOR: red">                          runat</span>="<span style="COLOR: dodgerblue">server</span>" <br />                          <span style="COLOR: red">DataSourceID</span>="<span style="COLOR: dodgerblue">SqlDataSource1</span>" <br />                          <span style="COLOR: red">Width</span>="<span style="COLOR: dodgerblue">100%</span>" <br />                          <span style="COLOR: red">OnCancelCommand</span>="<span style="COLOR: dodgerblue">DataList1_CancelCommand</span>" <br />                          <span style="COLOR: red">OnEditCommand</span>="<span style="COLOR: dodgerblue">DataList1_EditCommand</span>" <br />                          <span style="COLOR: red">OnUpdateCommand</span>="<span style="COLOR: dodgerblue">DataList1_UpdateCommand</span>" <br />                          <span style="COLOR: red">OnDeleteCommand</span>="<span style="COLOR: dodgerblue">DataList1_DeleteCommand</span>"<br />                          <span style="COLOR: red">OnItemCommand</span>="<span style="COLOR: dodgerblue">DataList1_ItemCommand</span>"<br />                          <span style="COLOR: red">RepeatLayout</span>="<span style="COLOR: dodgerblue">Flow</span>"  <span style="COLOR: blue">&gt;</span>
				<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">ItemTemplate</span><span style="COLOR: blue">&gt;</span>
				<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">asp:Panel</span> <span style="COLOR: red">ID</span>="<span style="COLOR: dodgerblue">contentPanel</span>" <br />                                  <span style="COLOR: red">runat</span>="<span style="COLOR: dodgerblue">server</span>" <br />                                  <span style="COLOR: red">Visible</span>='<font style="BACKGROUND-COLOR: yellow" color="black">&lt;%</font># Eval("<span style="COLOR: dodgerblue">IsVisible</span>") <font style="BACKGROUND-COLOR: yellow" color="black">%&gt;</font>'<span style="COLOR: blue">&gt;</span>
					<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">h3</span><span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">asp:Label</span> <span style="COLOR: red">ID</span>="<span style="COLOR: dodgerblue">HeadingLabel</span>" <br />                                              <span style="COLOR: red">runat</span>="<span style="COLOR: dodgerblue">server</span>" <br />                                              <span style="COLOR: red">Text</span>='<font style="BACKGROUND-COLOR: yellow" color="black">&lt;%</font># Eval("<span style="COLOR: dodgerblue">Heading</span>") <font style="BACKGROUND-COLOR: yellow" color="black">%&gt;</font>'<span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">asp:Label</span><span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">h3</span><span style="COLOR: blue">&gt;</span>
					<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">asp:Label</span> <span style="COLOR: red">ID</span>="<span style="COLOR: dodgerblue">ContentLabel</span>" <br />                                          <span style="COLOR: red">runat</span>="<span style="COLOR: dodgerblue">server</span>" <br />                                          <span style="COLOR: red">Text</span>='<font style="BACKGROUND-COLOR: yellow" color="black">&lt;%</font># Eval("<span style="COLOR: dodgerblue">Content</span>") <font style="BACKGROUND-COLOR: yellow" color="black">%&gt;</font>'<span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">asp:Label</span><span style="COLOR: blue">&gt;<br />                                        </span><span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">asp:HiddenField </span><span style="COLOR: red">ID</span>="<span style="COLOR: dodgerblue">hdnContentID</span>" <br />                                          <span style="COLOR: red">runat</span>="<span style="COLOR: dodgerblue">server</span>" <br />                                          <span style="COLOR: red">Value</span>='<font style="BACKGROUND-COLOR: yellow" color="black">&lt;%</font># Eval("<span style="COLOR: dodgerblue">Content_ID</span>") <font style="BACKGROUND-COLOR: yellow" color="black">%&gt;</font>' /<span style="COLOR: blue">&gt;</span>
					<span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">asp:Panel</span><span style="COLOR: blue">&gt;</span>
					<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">asp:Panel</span> <span style="COLOR: red">ID</span>="<span style="COLOR: dodgerblue">Panel1</span>" <br />                                          <span style="COLOR: red">Visible</span>='<font style="BACKGROUND-COLOR: yellow" color="black">&lt;%</font># User.IsInRole("<span style="COLOR: dodgerblue">Administrators</span>"<span style="COLOR: dodgerblue">) <font color="black"><font style="BACKGROUND-COLOR: yellow">%&gt;</font>'</font> <br />                                          <font color="red">runat</font><font color="black">=</font></span>"<span style="COLOR: dodgerblue">server</span>" <span style="COLOR: red">Height</span>="<span style="COLOR: dodgerblue">50px</span>" <span style="COLOR: red">Width</span>="<span style="COLOR: dodgerblue">125px</span>"<span style="COLOR: blue">&gt;</span>
					  <span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">asp:LinkButton</span> <span style="COLOR: red">ID</span>="<span style="COLOR: dodgerblue">LinkButton3</span>" <br />                                            <span style="COLOR: red">runat</span>="<span style="COLOR: dodgerblue">server</span>" <br />                                            <span style="COLOR: red">CommandName</span>="<span style="COLOR: dodgerblue">edit</span>"<span style="COLOR: blue">&gt;</span>Edit<span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">asp:LinkButton</span><span style="COLOR: blue">&gt;</span><font color="red">&amp;nbsp;&amp;nbsp;<br />                                          </font><span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">asp:LinkButton</span> <span style="COLOR: red">ID</span>="<span style="COLOR: dodgerblue">LinkButton4</span>" <br />                                            <span style="COLOR: red">runat</span>="<span style="COLOR: dodgerblue">server</span>" <br />                                            <span style="COLOR: red">CommandName</span>="<span style="COLOR: dodgerblue">delete</span>"<span style="COLOR: blue">&gt;</span>Delete<span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">asp:LinkButton</span><span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">asp:Panel</span><span style="COLOR: blue">&gt;</span>
				<span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">ItemTemplate</span><span style="COLOR: blue">&gt;</span>
				<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">SeparatorTemplate</span><span style="COLOR: blue">&gt;</span>
					<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">hr</span> /<span style="COLOR: blue">&gt;</span>
				<span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">SeparatorTemplate</span><span style="COLOR: blue">&gt;</span>
				<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">EditItemTemplate</span><span style="COLOR: blue">&gt;</span>
					<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">asp:TextBox</span> <span style="COLOR: red">ID</span>="<span style="COLOR: dodgerblue">txtHeading</span>" <br />                                          <span style="COLOR: red">runat</span>="<span style="COLOR: dodgerblue">server</span>" <br />                                          <span style="COLOR: red">Text</span>='<font style="BACKGROUND-COLOR: yellow" color="black">&lt;%</font># Bind("<span style="COLOR: dodgerblue">Heading</span>") <font style="BACKGROUND-COLOR: yellow" color="black">%&gt;</font>'<span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">asp:TextBox</span><span style="COLOR: blue">&gt;</span>
					<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">asp:CheckBox</span> <span style="COLOR: red">ID</span>="<span style="COLOR: dodgerblue">chkVisible</span>" <br />                                          <span style="COLOR: red">runat</span>="<span style="COLOR: dodgerblue">server</span>" <br />                                          <span style="COLOR: red">Checked</span>='<font style="BACKGROUND-COLOR: yellow" color="black">&lt;%</font># Bind("<span style="COLOR: dodgerblue">IsVisible</span>"<span style="COLOR: dodgerblue">) <font style="BACKGROUND-COLOR: yellow" color="black">%&gt;</font>' <br />                                          <font color="red">Text</font><font color="black">=</font></span>"<span style="COLOR: dodgerblue">Visible</span>" /<span style="COLOR: blue">&gt;<br /></span>
					ContentID:<br />                                        <span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">asp:Label</span> <span style="COLOR: red">ID</span>="<span style="COLOR: dodgerblue">lblContentID</span>" <br />                                          <span style="COLOR: red">runat</span>="<span style="COLOR: dodgerblue">server</span>" <br />                                          <span style="COLOR: red">Text</span>='<font style="BACKGROUND-COLOR: yellow" color="black">&lt;%</font># Eval("<span style="COLOR: dodgerblue">Content_ID</span>") <font style="BACKGROUND-COLOR: yellow" color="black">%&gt;</font>'<span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">asp:Label</span><span style="COLOR: blue">&gt;</span>
					<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">asp:TextBox</span> <span style="COLOR: red">ID</span>="<span style="COLOR: dodgerblue">txtContent</span>" <br />                                          <span style="COLOR: red">runat</span>="<span style="COLOR: dodgerblue">server</span>" <br />                                          <span style="COLOR: red">Columns</span>="<span style="COLOR: dodgerblue">40</span>" <span style="COLOR: red">Rows</span>="<span style="COLOR: dodgerblue">20</span>" <br />                                          <span style="COLOR: red">Text</span>='<font style="BACKGROUND-COLOR: yellow">&lt;%</font># Bind("<span style="COLOR: dodgerblue">Content</span>"<span style="COLOR: dodgerblue">) <font style="BACKGROUND-COLOR: yellow" color="black">%&gt;</font>'
					  <font color="red">TextMode</font><font color="black">=</font></span>"<span style="COLOR: dodgerblue">MultiLine</span>"<span style="COLOR: blue">&gt;</span><span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">asp:TextBox</span><span style="COLOR: blue">&gt;<br />                                        </span><span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">br</span> /<span style="COLOR: blue">&gt;</span>
					<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">br</span> /<span style="COLOR: blue">&gt;</span>
					<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">asp:LinkButton</span> <span style="COLOR: red">ID</span>="<span style="COLOR: dodgerblue">LinkButton1</span>" <br />                                          <span style="COLOR: red">runat</span>="<span style="COLOR: dodgerblue">server</span>" <br />                                          <span style="COLOR: red">CommandName</span>="<span style="COLOR: dodgerblue">update</span>"<span style="COLOR: blue">&gt;</span>Update<span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">asp:LinkButton</span><span style="COLOR: blue">&gt;</span><font color="red">&amp;nbsp;&amp;nbsp;</font>
					<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">asp:LinkButton</span> <span style="COLOR: red">ID</span>="<span style="COLOR: dodgerblue">LinkButton2</span>" <br />                                          <span style="COLOR: red">runat</span>="<span style="COLOR: dodgerblue">server</span>" <br />                                          <span style="COLOR: red">CausesValidation</span>="<span style="COLOR: dodgerblue">False</span>" <br />                                          <span style="COLOR: red">CommandName</span>="<span style="COLOR: dodgerblue">cancel</span>"<span style="COLOR: blue">&gt;</span>Cancel<span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">asp:LinkButton</span><span style="COLOR: blue">&gt;</span><font color="red">&amp;nbsp;&amp;nbsp;</font>
					<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">asp:LinkButton</span> <span style="COLOR: red">ID</span>="<span style="COLOR: dodgerblue">LinkButton5</span>" <br />                                          <span style="COLOR: red">runat</span>="<span style="COLOR: dodgerblue">server</span>" <br />                                          <span style="COLOR: red">CommandName</span>="<span style="COLOR: dodgerblue">add</span>"<span style="COLOR: blue">&gt;</span>Create as New<span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">asp:LinkButton</span><span style="COLOR: blue">&gt;</span>
				<span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">EditItemTemplate</span><span style="COLOR: blue">&gt;</span>
			<span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">asp:DataList</span><span style="COLOR: blue">&gt;</span></pre>
			
Several points of interest in the DataList declaration:
<ul>
  <li>
  <div>No more pesky DataBinder.Eval(Container.DataItem, "field") syntax - much 
  leaner and meaner Eval() syntax for one-way binding.</div>
  </li><li>
  <div>Two-way binding happens via the Bind() syntax - notice that Bind() only 
  happens in the EditItemTemplate, since the ItemTemplate is readonly.</div>
  </li><li>
  <div>I'm only showing the edit/delete buttons based on what role the current 
  user is in. I wasn't sure if this (# 
  User.IsInRole("Administrators")) would work at first because it's 
  deceptively simple. But yeah, it does work. Works great!</div>
  </li><li>
  <div>I did most of this visually - there is no longer a reason to fear the 
  designer in asp.net (thanks Venus team!)</div>
  </li><li>
  <div>I had to disable Page input validation because I want the Content to 
  contain html, and by default, it don't like that.</div></li></ul>

As for the codebehind, I guess I could have refactored it a little bit, but 
since this is not a mission-critical application (it is just a personal site, 
after all!) I just went the easy route and duplicated a lot of code. Probably 
the best thing to do would be to handle just the ItemCommand because there is no 
default handler for add and use a clever mix of a switch statement and 
defaulting the value of EditItemIndex to -1. But this isn't about best 
practices, it's about getting the stuff to work, ya know? Anyway, here's the 
code:

<pre><span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  1</span> 	<span style="COLOR: blue">protected</span> <span style="COLOR: blue">void</span> DataList1_CancelCommand(<span style="COLOR: blue">object</span> source, DataListCommandEventArgs e)
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  2</span> 	{
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  3</span> 		<span style="COLOR: blue">this</span>.DataList1.EditItemIndex = -<span style="COLOR: maroon">1</span>;
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  4</span> 		<span style="COLOR: blue">this</span>.DataList1.DataBind();
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  5</span> 	}
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  6</span> 	<span style="COLOR: blue">protected</span> <span style="COLOR: blue">void</span> DataList1_UpdateCommand(<span style="COLOR: blue">object</span> source, DataListCommandEventArgs e)
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  7</span> 	{
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  8</span> 		<span style="COLOR: blue">string</span> heading = ((TextBox)e.Item.FindControl(<span style="COLOR: maroon">"txtHeading"</span>)).Text;
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey">  9</span> 		<span style="COLOR: blue">string</span> content = ((TextBox)e.Item.FindControl(<span style="COLOR: maroon">"txtContent"</span>)).Text;
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 10</span> 		<span style="COLOR: blue">string</span> isvisible = ((CheckBox)e.Item.FindControl(<span style="COLOR: maroon">"chkVisible"</span>)).Checked.ToString();
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 11</span> 		<span style="COLOR: blue">string</span> id = ((Label)e.Item.FindControl(<span style="COLOR: maroon">"lblContentID"</span>)).Text;
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 12</span> 
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 13</span> 		<span style="COLOR: blue">this</span>.SqlDataSource1.UpdateParameters[<span style="COLOR: maroon">"Content_ID"</span>].DefaultValue = id;
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 14</span> 		<span style="COLOR: blue">this</span>.SqlDataSource1.UpdateParameters[<span style="COLOR: maroon">"Heading"</span>].DefaultValue = heading;
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 15</span> 		<span style="COLOR: blue">this</span>.SqlDataSource1.UpdateParameters[<span style="COLOR: maroon">"Content"</span>].DefaultValue = content;
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 16</span> 		<span style="COLOR: blue">this</span>.SqlDataSource1.UpdateParameters[<span style="COLOR: maroon">"IsVisible"</span>].DefaultValue = isvisible;
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 17</span> 
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 18</span> 		<span style="COLOR: blue">this</span>.SqlDataSource1.Update();
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 19</span> 
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 20</span> 		<span style="COLOR: blue">this</span>.DataList1.EditItemIndex = -<span style="COLOR: maroon">1</span>;
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 21</span> 		<span style="COLOR: blue">this</span>.DataList1.DataBind();
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 22</span> 	}
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 23</span> 	<span style="COLOR: blue">protected</span> <span style="COLOR: blue">void</span> DataList1_DeleteCommand(<span style="COLOR: blue">object</span> source, DataListCommandEventArgs e)
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 24</span> 	{
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 25</span> 		<span style="COLOR: blue">string</span> id = ((HiddenField)e.Item.FindControl(<span style="COLOR: maroon">"hdnContentID"</span>)).Value;
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 26</span> 		<span style="COLOR: blue">this</span>.SqlDataSource1.DeleteParameters[<span style="COLOR: maroon">"Content_ID"</span>].DefaultValue = id;
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 27</span> 
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 28</span> 		<span style="COLOR: blue">this</span>.SqlDataSource1.Delete();
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 29</span> 
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 30</span> 		<span style="COLOR: blue">this</span>.DataList1.EditItemIndex = -<span style="COLOR: maroon">1</span>;
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 31</span> 		<span style="COLOR: blue">this</span>.DataList1.DataBind();
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 32</span> 	}
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 33</span> 	<span style="COLOR: blue">protected</span> <span style="COLOR: blue">void</span> DataList1_ItemCommand(<span style="COLOR: blue">object</span> source, DataListCommandEventArgs e)
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 34</span> 	{
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 35</span> 		<span style="COLOR: blue">switch</span> (e.CommandName)
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 36</span> 		{
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 37</span> 			<span style="COLOR: blue">case</span> <span style="COLOR: maroon">"add"</span>:
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 38</span> 				<span style="COLOR: blue">string</span> heading = ((TextBox)e.Item.FindControl(<span style="COLOR: maroon">"txtHeading"</span>)).Text;
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 39</span> 				<span style="COLOR: blue">string</span> content = ((TextBox)e.Item.FindControl(<span style="COLOR: maroon">"txtContent"</span>)).Text;
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 40</span> 				<span style="COLOR: blue">string</span> isvisible = ((CheckBox)e.Item.FindControl(<span style="COLOR: maroon">"chkVisible"</span>)).Checked.ToString();
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 41</span> 
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 42</span> 				<span style="COLOR: blue">this</span>.SqlDataSource1.InsertParameters[<span style="COLOR: maroon">"Heading"</span>].DefaultValue = heading;
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 43</span> 				<span style="COLOR: blue">this</span>.SqlDataSource1.InsertParameters[<span style="COLOR: maroon">"Content"</span>].DefaultValue = content;
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 44</span> 				<span style="COLOR: blue">this</span>.SqlDataSource1.InsertParameters[<span style="COLOR: maroon">"IsVisible"</span>].DefaultValue = isvisible;
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 45</span> 
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 46</span> 				<span style="COLOR: blue">this</span>.SqlDataSource1.Insert();
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 47</span> 
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 48</span> 				<span style="COLOR: blue">this</span>.DataList1.EditItemIndex = -<span style="COLOR: maroon">1</span>;
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 49</span> 				<span style="COLOR: blue">this</span>.DataList1.DataBind();
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 50</span> 				<span style="COLOR: blue">break</span>;
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 51</span> 		}
<span style="COLOR: teal; BACKGROUND-COLOR: lightgrey"> 52</span> 	}</pre>

This is the quickest way I could figure out to make things work, and yeah, it 
does work. So, there you have it - even though there are only two items 
currently in the table, it's very easy to add content via in-place editing and 
change what is currently there as well. You can view it live over at <a href="http://www.bluefenix.net">www.bluefenix.net</a>.

<p class="media">[ Currently Playing : Voices - Godsmack - Other Side (3:44) 
]</p>