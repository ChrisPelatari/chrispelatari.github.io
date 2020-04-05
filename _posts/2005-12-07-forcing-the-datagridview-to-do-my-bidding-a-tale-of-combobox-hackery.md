---
layout: post
title: Forcing the DataGridView to do my bidding - a tale of ComboBox hackery
date: 2005-12-07 20:38
author: chrispelatari
comments: true
categories: [professional_geek]
---

<p><strong>*sigh* </strong>Winforms team, winforms team, when will you start 
making my life easier? As <a href="http://angrypets.com/blog/posts/554.aspx">others have said</a> (and I 
<a href="http://www.chrisfrazier.net/blog/archive/2005/09/07/1318.aspx">completely 
agree </a>) windowsforms.net is pretty useless. Well, there's some new 
<strike>Whidbey</strike> .NET 2.0 content, but all of the things I enjoyed when 
starting w/ v1 of .NET (like, erm, QuickStarts? What happened to installing 
those locally?) seem to be gone. To be fair, they do have a presence over on <a href="http://forums.microsoft.com/MSDN/default.aspx?ForumGroupID=2&amp;SiteID=1">forums.microsoft.com</a> where 
there are a few PM's and devs answering questions. I even found a 
<strike>hack</strike> fix for my dilemma via one of the posts that links to a <a href="http://download.microsoft.com/download/c/8/b/c8bc8bfe-30e6-417d-8c42-1bbf714bf976/VS05-01MacDonald.exe">download</a> 
from Beta 2 or somewhere close.</p>
<p>At first I was optimistic about the DataGridView samples (<a href="http://www.windowsforms.net/WhidbeyFeatures/default.aspx?PageID=2&amp;ItemID=13&amp;Cat=Controls&amp;tabindex=5">overview</a>)(<a href="http://www.windowsforms.net/Samples/download.aspx?PageId=1&amp;ItemId=220&amp;tabindex=4">Download 
The DataGridView samples</a>), but I didn't see anything that did what I wanted 
to do: take an enum value and represent it in the grid with a combobox. So, 
here's how I did it.</p>
<p>First, I just plopped a DataGridView onto a form and gave it a BindingSource. 
The bindingSource gets its DataSource property set via a call into my DAL that 
returns a DataTable:</p><pre><span style="color:green;">//CF: set to null before setting it to the current to 
</span><span style="color:green;">//clear out previous results
</span><span style="color:blue;">this</span>.bindingSource1.DataSource = <span style="color:blue;">null</span>;

<span style="color:blue;">this</span>.bindingSource1.DataSource = MyDal.GetDataTable();</pre>
<p>Then comes the hackery. Since I have about 20 columns in this DataTable, all 
of interest as far as values but not all needing to be visible, directly after 
(like the line after) setting the datasource, I call a method to format the 
grid. This method looks something like this:</p><pre><span style="color:blue;">private</span> <span style="color:blue;">void</span> _formatGrid(){
	<span style="color:blue;">this</span>.dataGridView1.Columns[<span style="color:maroon;">"ID"</span>].Visible = <span style="color:maroon;">false</span>;
	<span style="color:blue;">this</span>.dataGridView1.Columns.Remove(<span style="color:maroon;">"Status"</span>);<span style="color:green;">//CF: this is where we want enums.
</span>	...
	<span style="color:blue;">this</span>._formatStatusColumn();
}</pre>
<p>Then the _formatStatusColumn method is where the magick happens:</p><pre>DataTable dt = <span style="color:blue;">new</span> DataTable(<span style="color:maroon;">"Status"</span>);

<span style="color:green;">//CF: actually how it's stored in the db.
</span>dt.Columns.Add(<span style="color:maroon;">"Status"</span>, <span style="color:blue;">typeof</span>(<span style="color:blue;">int</span>)); 
dt.Columns.Add(<span style="color:maroon;">"Status_Name"</span>, <span style="color:blue;">typeof</span>(<span style="color:blue;">string</span>));

<span style="color:green;">//CF: this way I can add or remove enum values, and
</span><span style="color:green;">//the combo will always reflect the correct values.
</span><span style="color:blue;">foreach</span>(<span style="color:blue;">int</span> index <span style="color:blue;">in</span> Enum.GetValues(<span style="color:blue;">typeof</span>(Status)){
	dt.Rows.Add(index, Enum.GetName(<span style="color:blue;">typeof</span>(Status), index));
}

<span style="color:green;">//CF: now for the UI column
</span>DataGridViewComboBoxColumn statusColumn = 
	<span style="color:blue;">new</span> DataGridViewComboBoxColumn();

<span style="color:green;">//CF: seems to control where the column is placed.
</span>statusColumn.DisplayIndex = <span style="color:maroon;">3</span>;
statusColumn.HeaderText = <span style="color:maroon;">"Status"</span>;

statusColumn.DataPropertyName = <span style="color:maroon;">"Status"</span>;
statusColumn.DataSource = dt;
statusColumn.DisplayMember = <span style="color:maroon;">"Status_Name"</span>;
statusColumn.ValueMember = <span style="color:maroon;">"Status"</span>;

<span style="color:blue;">this</span>.dataGridView1.Columns.Add(statusColumn);</pre>
<p>I was <em>hoping</em> that there would be some way to predefine columns so I 
don't have to filter and rebuild every time I get data from the database, but I 
couldn't find anything on it. There is no SelectedIndex member of the 
DataGridViewComboBoxCell, either.</p>
<p>I really hope this helps someone else out there: I tried for a day and a half 
to get this to work, and I still think it looks like a hack.</p>
