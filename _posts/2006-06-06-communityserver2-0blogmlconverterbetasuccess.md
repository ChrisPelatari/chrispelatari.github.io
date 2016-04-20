---
layout: post
title: Community Server 2.0 BlogML Converter Beta - success!
date: 2006-06-06 13:32
author: chrispelatari
comments: true
categories: [Uncategorized]
---

<p>I'm a little bit behind on my CS releases, as I just got around to installing 
a fresh copy of Community Server 2.0 to test things out for one of my sites. 
Since I was going to upgrade an existing CS 1.1 install, I tried that method 
first, but ended up starting over because the original config I had was single 
blog and I didn't have the time nor the patience to figure out how to hack 2.0 
into a single-blog install with existing content.</p>
<p>However, thanks to <a href="http://nayyeri.net/archive/2006/02/11/491.aspx">Keyvan</a> (che 
khabbar!), I was able to export the 1.1 content using an HttpHandler I hacked up 
for exporting CS 1.1 content to BlogML and import into a new, multi-blog install 
of 2.0. The first thing I did was nuke both the sample weblog and the sample 
weblog group. Then I created a new group and weblog and used the application key 
assigned to the new blog to import my posts. Here is the code I used to import a 
blogML file into a fresh copy of Community Server 2.0</p><pre><span style="color:blue;">&lt;</span><span style="color:maroon;">%@</span> Page <span style="color:red;">Language</span>="<span style="color:dodgerblue;">VB</span>" %<span style="color:blue;">&gt;</span>
<span style="color:blue;">&lt;</span><span style="color:maroon;">%@</span> Import <span style="color:red;">Namespace</span>="<span style="color:dodgerblue;">System.Collections</span>"%<span style="color:blue;">&gt;</span>
<span style="color:blue;">&lt;</span><span style="color:maroon;">%@</span> Import <span style="color:red;">Namespace</span>="<span style="color:dodgerblue;">System.IO</span>"%<span style="color:blue;">&gt;</span>
<span style="color:blue;">&lt;</span><span style="color:maroon;">%@</span> Import <span style="color:red;">Namespace</span>="<span style="color:dodgerblue;">BlogML</span>"%<span style="color:blue;">&gt;</span>
<span style="color:blue;">&lt;</span><span style="color:maroon;">%@</span> Import <span style="color:red;">Namespace</span>="<span style="color:dodgerblue;">BlogML.Xml</span>"%<span style="color:blue;">&gt;</span>
<span style="color:blue;">&lt;</span><span style="color:maroon;">%@</span> Import <span style="color:red;">Namespace</span>="<span style="color:dodgerblue;">CommunityServer</span>"%<span style="color:blue;">&gt;</span>
<span style="color:blue;">&lt;</span><span style="color:maroon;">%@</span> Import <span style="color:red;">Namespace</span>="<span style="color:dodgerblue;">CommunityServer.Components</span>"%<span style="color:blue;">&gt;</span>
<span style="color:blue;">&lt;</span><span style="color:maroon;">%@</span> Import <span style="color:red;">Namespace</span>="<span style="color:dodgerblue;">CommunityServer.Blogs</span>"%<span style="color:blue;">&gt;</span>
<span style="color:blue;">&lt;</span><span style="color:maroon;">script</span> <span style="color:red;">runat</span>="<span style="color:dodgerblue;">server</span>"<span style="color:blue;">&gt;</span>
</pre><pre><span style="color:green;">'Community Server 2.0 BlogML converter Beta
</span><span style="color:green;">'Copyright Keyvan Nayyeri (www.nayyeri.net) - 2006
</span><span style="color:green;">'BlogML Writer and Reader classes are provided by BlogML project (www.blogml.com)
</span>

    <span style="color:blue;">Public</span> <span style="color:blue;">Class</span> Reader

        <span style="color:blue;">Private</span> _ApplicationKey <span style="color:blue;">As</span> <span style="color:blue;">String</span>
        <span style="color:blue;">Private</span> _Blog <span style="color:blue;">As</span> CommunityServer.Blogs.Components.Weblog
        <span style="color:blue;">Private</span> _SitePath <span style="color:blue;">As</span> <span style="color:blue;">String</span>
        <span style="color:blue;">Private</span> _BlogCommentCount <span style="color:blue;">As</span> <span style="color:blue;">Integer</span>
        <span style="color:blue;">Private</span> _BlogTrackBackCount <span style="color:blue;">As</span> <span style="color:blue;">Integer</span>

        <span style="color:blue;">Sub</span> <span style="color:blue;">New</span>(<span style="color:blue;">ByVal</span> ApplicationKey <span style="color:blue;">As</span> <span style="color:blue;">String</span>, <span style="color:blue;">ByVal</span> SitePath <span style="color:blue;">As</span> <span style="color:blue;">String</span>)
            <span style="color:blue;">Me</span>._ApplicationKey = ApplicationKey
            <span style="color:blue;">Me</span>._SitePath = SitePath


            <span style="color:blue;">Dim</span> objCSWeblogs <span style="color:blue;">As</span> CommunityServer.Blogs.Components.Weblogs
            <span style="color:blue;">Me</span>._Blog = objCSWeblogs.GetWeblog(<span style="color:blue;">Me</span>._ApplicationKey)
        <span style="color:blue;">End</span> <span style="color:blue;">Sub</span>

        <span style="color:blue;">Public</span> <span style="color:blue;">Sub</span> LoadBlog(<span style="color:blue;">ByVal</span> XML <span style="color:blue;">As</span> <span style="color:blue;">String</span>)
            <span style="color:blue;">Dim</span> Blog <span style="color:blue;">As</span> <span style="color:blue;">New</span> BlogMLBlog
            <span style="color:blue;">Try</span>
                Blog = BlogMLSerializer.Deserialize(<span style="color:blue;">New</span> StringReader(XML))
            <span style="color:blue;">Catch</span> ex <span style="color:blue;">As</span> Exception
                <span style="color:blue;">Throw</span> <span style="color:blue;">New</span> Exception(<span style="color:maroon;">"Couldn't load your BlogML file. Maybe it is wellformedness"</span>)
            <span style="color:blue;">End</span> <span style="color:blue;">Try</span>
            <span style="color:blue;">Dim</span> Categories <span style="color:blue;">As</span> Hashtable
            Categories = ReadCategories(Blog)

            LoadPosts(Blog, Categories)

            UpdateStats(Blog)
        <span style="color:blue;">End</span> <span style="color:blue;">Sub</span>

        <span style="color:blue;">Private</span> <span style="color:blue;">Function</span> ReadCategories(<span style="color:blue;">ByVal</span> Blog <span style="color:blue;">As</span> BlogMLBlog) <span style="color:blue;">As</span> Hashtable
            <span style="color:blue;">Dim</span> CategoriesHash <span style="color:blue;">As</span> <span style="color:blue;">New</span> Hashtable
            <span style="color:blue;">For</span> <span style="color:blue;">Each</span> Category <span style="color:blue;">As</span> BlogMLCategory <span style="color:blue;">In</span> Blog.Categories
                <span style="color:blue;">Dim</span> NewCategory <span style="color:blue;">As</span> <span style="color:blue;">New</span> PostCategory
                <span style="color:blue;">With</span> NewCategory
                    .DateCreated = Category.DateCreated
                    .Description = Category.Description
                    .IsEnabled = Category.Approved
                    .Name = Category.Title
                    .ParentID = <span style="color:maroon;">0</span>
                    .SectionID = <span style="color:blue;">Me</span>._Blog.SectionID

                    <span style="color:blue;">Dim</span> objCSCats <span style="color:blue;">As</span> PostCategories
                    <span style="color:blue;">Try</span>
                        objCSCats.CreateCategory(NewCategory)
                    <span style="color:blue;">Catch</span> ex <span style="color:blue;">As</span> Exception
                        <span style="color:blue;">Throw</span> <span style="color:blue;">New</span> ArgumentException(<span style="color:maroon;">"Error when tried to add categories to database"</span>)
                    <span style="color:blue;">End</span> <span style="color:blue;">Try</span>
                    CategoriesHash.Add(Category.ID, Category.Title)
                <span style="color:blue;">End</span> <span style="color:blue;">With</span>
            <span style="color:blue;">Next</span>
            <span style="color:blue;">Return</span> CategoriesHash
        <span style="color:blue;">End</span> <span style="color:blue;">Function</span>
        <span style="color:blue;">Private</span> <span style="color:blue;">Sub</span> LoadPosts(<span style="color:blue;">ByVal</span> Blog <span style="color:blue;">As</span> BlogMLBlog, <span style="color:blue;">ByVal</span> CategoryHash <span style="color:blue;">As</span> Hashtable)
            <span style="color:blue;">Dim</span> LastPostAuthor <span style="color:blue;">As</span> <span style="color:blue;">String</span>
            <span style="color:blue;">Dim</span> LastPostAuthorID <span style="color:blue;">As</span> <span style="color:blue;">Integer</span>
            <span style="color:blue;">Dim</span> LastPostDate <span style="color:blue;">As</span> <span style="color:blue;">Date</span>
            <span style="color:blue;">Dim</span> LastPostName <span style="color:blue;">As</span> <span style="color:blue;">String</span>
            <span style="color:blue;">Dim</span> LastPostSubject <span style="color:blue;">As</span> <span style="color:blue;">String</span>




            <span style="color:blue;">For</span> <span style="color:blue;">Each</span> Post <span style="color:blue;">As</span> BlogMLPost <span style="color:blue;">In</span> Blog.Posts
                <span style="color:blue;">Dim</span> NewPost <span style="color:blue;">As</span> <span style="color:blue;">New</span> CommunityServer.Blogs.Components.WeblogPost
                <span style="color:blue;">Dim</span> objCSPosts <span style="color:blue;">As</span> CommunityServer.Blogs.Components.WeblogPosts

                <span style="color:blue;">With</span> NewPost
                    .PostID = Post.ID
                    .Body = Post.Content.UncodedText
                    .BlogPostType = CommunityServer.Blogs.Components.BlogPostType.Post
                    .Subject = Post.Title
                    .ThreadDate = Post.DateCreated
                    .UserTime = Post.DateCreated
                    .PostDate = Post.DateCreated
                    .UserTime = Post.DateCreated
                    .SectionID = <span style="color:blue;">Me</span>._Blog.SectionID
                    .SetExtendedAttribute(<span style="color:maroon;">"EverPublished"</span>, <span style="color:blue;">CType</span>(Post.Approved, <span style="color:blue;">Boolean</span>))
                    .IndexInThread = <span style="color:maroon;">True</span>
                    .IsApproved = <span style="color:maroon;">True</span>
                    .IsAggregated = <span style="color:maroon;">True</span>
                    .IsLocked = <span style="color:maroon;">False</span>
                    .PostConfig = CommunityServer.Blogs.Components.BlogPostConfig.IsAggregated

                <span style="color:blue;">End</span> <span style="color:blue;">With</span>
                <span style="color:green;">'Add categories
</span>                <span style="color:blue;">If</span> Post.Categories.Count &gt; <span style="color:maroon;">0</span> <span style="color:blue;">Then</span>
                    <span style="color:blue;">Dim</span> NewPostCats(Post.Categories.Count) <span style="color:blue;">As</span> <span style="color:blue;">String</span>
                    <span style="color:blue;">For</span> i <span style="color:blue;">As</span> <span style="color:blue;">Integer</span> = <span style="color:maroon;">0</span> <span style="color:blue;">To</span> Post.Categories.Count - <span style="color:maroon;">1</span>
                        NewPostCats(i) = CategoryHash(Post.Categories(i).Ref)
                    <span style="color:blue;">Next</span>
                    NewPost.Categories = NewPostCats
                <span style="color:blue;">End</span> <span style="color:blue;">If</span>

                <span style="color:green;">'Add attachments
</span>                <span style="color:green;">'TO DO: Check to add attachments with checking the source code when RTM version has been released.
</span>                <span style="color:green;">'Currently we can't load post attachments</span>

                objCSPosts.Add(NewPost)

                <span style="color:green;">'Temporary saving stats
</span>                LastPostAuthor = NewPost.Username
                LastPostAuthorID = NewPost.AuthorID
                LastPostDate = NewPost.PostDate
                LastPostName = NewPost.Name
                LastPostSubject = NewPost.Subject

                LoadComments(NewPost, Post)
                LoadTrackBacks(NewPost, Post)
            <span style="color:blue;">Next</span>

            <span style="color:green;">'Update blog stats
</span>            <span style="color:blue;">Me</span>._Blog.MostRecentPostAuthor = LastPostAuthor
            <span style="color:blue;">Me</span>._Blog.MostRecentPostAuthorID = LastPostAuthorID
            <span style="color:blue;">Me</span>._Blog.MostRecentPostDate = LastPostDate
            <span style="color:blue;">Me</span>._Blog.MostRecentPostName = LastPostName
            <span style="color:blue;">Me</span>._Blog.MostRecentPostSubject = LastPostSubject
        <span style="color:blue;">End</span> <span style="color:blue;">Sub</span>
        <span style="color:blue;">Private</span> <span style="color:blue;">Sub</span> LoadComments(<span style="color:blue;">ByVal</span> NewPost <span style="color:blue;">As</span> Post, <span style="color:blue;">ByVal</span> Post <span style="color:blue;">As</span> BlogMLPost)
            <span style="color:blue;">If</span> Post.Comments.Count &gt; <span style="color:maroon;">0</span> <span style="color:blue;">Then</span>
                <span style="color:blue;">For</span> <span style="color:blue;">Each</span> Comment <span style="color:blue;">As</span> BlogMLComment <span style="color:blue;">In</span> Post.Comments
                    <span style="color:blue;">Dim</span> NewComment <span style="color:blue;">As</span> <span style="color:blue;">New</span> CommunityServer.Blogs.Components.WeblogPost
                    <span style="color:blue;">Dim</span> objCSComments <span style="color:blue;">As</span> CommunityServer.Blogs.Components.WeblogPosts

                    <span style="color:blue;">With</span> NewComment
                        .Body = Comment.Content.UncodedText
                        .BlogPostType = Blogs.Components.BlogPostType.Comment
                        .Subject = Comment.Title
                        .ThreadDate = Comment.DateCreated
                        .UserTime = Comment.DateCreated
                        .PostDate = Comment.DateCreated
                        .UserTime = Comment.DateCreated
                        .SectionID = <span style="color:blue;">Me</span>._Blog.SectionID
                        .SetExtendedAttribute(<span style="color:maroon;">"EverPublished"</span>, <span style="color:maroon;">True</span>)
                        .SetExtendedAttribute(<span style="color:maroon;">"TitleUrl"</span>, Comment.UserUrl)
                        .SetExtendedAttribute(<span style="color:maroon;">"SubmittedUserName"</span>, Comment.UserName)
                        .IsApproved = <span style="color:blue;">CType</span>(Comment.Approved, <span style="color:blue;">Boolean</span>)
                        .ParentID = NewPost.PostID
                        .ThreadID = NewPost.ThreadID

                    <span style="color:blue;">End</span> <span style="color:blue;">With</span>

                    objCSComments.Add(NewComment)

                    <span style="color:green;">'Update blog counter
</span>                    <span style="color:blue;">Me</span>._BlogCommentCount += <span style="color:maroon;">1</span>
                <span style="color:blue;">Next</span>
            <span style="color:blue;">End</span> <span style="color:blue;">If</span>
        <span style="color:blue;">End</span> <span style="color:blue;">Sub</span>
        <span style="color:blue;">Private</span> <span style="color:blue;">Sub</span> LoadTrackBacks(<span style="color:blue;">ByVal</span> NewPost <span style="color:blue;">As</span> Post, <span style="color:blue;">ByVal</span> Post <span style="color:blue;">As</span> BlogMLPost)
            <span style="color:blue;">If</span> Post.Trackbacks.Count &gt; <span style="color:maroon;">0</span> <span style="color:blue;">Then</span>
                <span style="color:blue;">For</span> <span style="color:blue;">Each</span> TrackBack <span style="color:blue;">As</span> BlogMLTrackback <span style="color:blue;">In</span> Post.Trackbacks
                    <span style="color:blue;">Dim</span> NewTrackBack <span style="color:blue;">As</span> <span style="color:blue;">New</span> Blogs.Components.WeblogPost
                    <span style="color:blue;">Dim</span> objCSTrackBacks <span style="color:blue;">As</span> Blogs.Components.WeblogPosts

                    <span style="color:blue;">With</span> NewTrackBack
                        .Body = TrackBack.Title
                        .BlogPostType = Blogs.Components.BlogPostType.Trackback
                        .Subject = TrackBack.Title
                        .ThreadDate = TrackBack.DateCreated
                        .UserTime = TrackBack.DateCreated
                        .PostDate = TrackBack.DateCreated
                        .UserTime = TrackBack.DateCreated
                        .SectionID = <span style="color:blue;">Me</span>._Blog.SectionID
                        .SetExtendedAttribute(<span style="color:maroon;">"EverPublished"</span>, <span style="color:maroon;">True</span>)
                        .SetExtendedAttribute(<span style="color:maroon;">"TitleUrl"</span>, TrackBack.Url)
                        .SetExtendedAttribute(<span style="color:maroon;">"trackbackName"</span>, <span style="color:maroon;">"TrackBack"</span>)
                        .IsApproved = <span style="color:blue;">CType</span>(TrackBack.Approved, <span style="color:blue;">Boolean</span>)
                        .ParentID = NewPost.PostID
                        .ThreadID = NewPost.ThreadID

                    <span style="color:blue;">End</span> <span style="color:blue;">With</span>

                    objCSTrackBacks.Add(NewTrackBack)

                    <span style="color:green;">'Update blog counter
</span>                    <span style="color:blue;">Me</span>._BlogTrackBackCount += <span style="color:maroon;">1</span>
                <span style="color:blue;">Next</span>
            <span style="color:blue;">End</span> <span style="color:blue;">If</span>
        <span style="color:blue;">End</span> <span style="color:blue;">Sub</span>
        <span style="color:blue;">Private</span> <span style="color:blue;">Sub</span> UpdateStats(<span style="color:blue;">ByVal</span> Blog <span style="color:blue;">As</span> BlogMLBlog)
            <span style="color:blue;">Me</span>._Blog.PostCount += Blog.Posts.Count
            <span style="color:blue;">Me</span>._Blog.CommentCount = <span style="color:blue;">Me</span>._BlogCommentCount
            <span style="color:blue;">Me</span>._Blog.TrackbackCount = <span style="color:blue;">Me</span>._BlogTrackBackCount
        <span style="color:blue;">End</span> <span style="color:blue;">Sub</span>

    <span style="color:blue;">End</span> <span style="color:blue;">Class</span>

    <span style="color:blue;">Sub</span> Page_Load(sender <span style="color:blue;">as</span> <span style="color:blue;">Object</span>, e <span style="color:blue;">as</span> EventArgs)
    	<span style="color:blue;">Dim</span> Path <span style="color:blue;">as</span> <span style="color:blue;">String</span> = <span style="color:maroon;">"d:tmpBlogMLBlogML.xml"</span>
    	<span style="color:blue;">Dim</span> reader <span style="color:blue;">as</span> <span style="color:blue;">New</span> Reader(<span style="color:maroon;">"chris"</span>, Request.PhysicalApplicationPath)

    	<span style="color:blue;">If</span> File.Exists(Path) <span style="color:blue;">Then</span>
    		<span style="color:blue;">Dim</span> sr <span style="color:blue;">as</span> <span style="color:blue;">New</span> StreamReader(File.Open(Path, FileMode.Open))
    		<span style="color:blue;">Dim</span> xml <span style="color:blue;">as</span> <span style="color:blue;">string</span> = sr.ReadToEnd

    		reader.LoadBlog(xml)

    		Response.Write(<span style="color:maroon;">"Content moved successfully!"</span>)
    	<span style="color:blue;">Else</span>
    		Response.Write(<span style="color:maroon;">"Uh-oh. Something crapped."</span>)
    	<span style="color:blue;">End</span> <span style="color:blue;">If</span>

    <span style="color:blue;">End</span> <span style="color:blue;">Sub</span>

<pre><span style="color:blue;">&lt;</span>/<span style="color:maroon;">script</span><span style="color:blue;">&gt;</span>
<span style="color:blue;">&lt;</span><span style="color:maroon;">html</span><span style="color:blue;">&gt;</span>
    <span style="color:blue;">&lt;</span><span style="color:maroon;">head</span><span style="color:blue;">&gt;</span>
    <span style="color:blue;">&lt;</span>/<span style="color:maroon;">head</span><span style="color:blue;">&gt;</span>
    <span style="color:blue;">&lt;</span><span style="color:maroon;">body</span><span style="color:blue;">&gt;</span>
        <span style="color:blue;">&lt;</span><span style="color:maroon;">form</span> <span style="color:red;">runat</span>="<span style="color:dodgerblue;">server</span>"<span style="color:blue;">&gt;</span>
            <span style="color:blue;">&lt;</span>!-- Insert content here --<span style="color:blue;">&gt;</span>
        <span style="color:blue;">&lt;</span>/<span style="color:maroon;">form</span><span style="color:blue;">&gt;</span>
    <span style="color:blue;">&lt;</span>/<span style="color:maroon;">body</span><span style="color:blue;">&gt;</span>
<span style="color:blue;">&lt;</span>/<span style="color:maroon;">html</span><span style="color:blue;">&gt;</span>
</pre></pre>
<p>I hacked up this file in WebMatrix and slapped it into the webroot of my new 
CommunityServer install. This way I was able to copy the content to a local 

install before pushing the final product out into the wild, and I didn't 
have to recompile any of CS to get it working. Merci, Keyvan!</p>
