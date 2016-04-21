---
layout: post
title: Community Server 2.0 BlogML Converter Beta - success!
date: 2006-06-06 13:32
author: chrispelatari
comments: true
categories: [aspnet,BlogML]
---

I'm a little bit behind on my CS releases, as I just got around to installing
a fresh copy of Community Server 2.0 to test things out for one of my sites.
Since I was going to upgrade an existing CS 1.1 install, I tried that method
first, but ended up starting over because the original config I had was single
blog and I didn't have the time nor the patience to figure out how to hack 2.0
into a single-blog install with existing content.

However, thanks to [Keyvan](http://nayyeri.net/archive/2006/02/11/491.aspx) (che
khabbar!), I was able to export the 1.1 content using an HttpHandler I hacked up
for exporting CS 1.1 content to BlogML and import into a new, multi-blog install
of 2.0. The first thing I did was nuke both the sample weblog and the sample
weblog group. Then I created a new group and weblog and used the application key
assigned to the new blog to import my posts. Here is the code I used to import a
blogML file into a fresh copy of Community Server 2.0

```ASP
<%@ Page Language = "VB" %>
<%@ Import Namespace = "System.Collections" %>
<%@ Import Namespace = "System.IO" %>
<%@ Import Namespace = "BlogML" %>
<%@ Import Namespace = "BlogML.Xml" %>
<%@ Import Namespace = "CommunityServer" %>
<%@ Import Namespace = "CommunityServer.Components" %>
<%@ Import Namespace = "CommunityServer.Blogs" %>

<script runat="server">
'Community Server 2.0 BlogML converter Beta
'Copyright Keyvan Nayyeri (www.nayyeri.net) - 2006
'BlogML Writer and Reader classes are provided by BlogML project (www.blogml.com)


Public Class Reader

  Private _ApplicationKey As String
  Private _Blog As CommunityServer.Blogs.Components.Weblog
  Private _SitePath As String
  Private _BlogCommentCount As Integer
  Private _BlogTrackBackCount As Integer

  Sub New(ByVal ApplicationKey As String, ByVal SitePath As String)
    Me._ApplicationKey = ApplicationKey
    Me._SitePath = SitePath


    Dim objCSWeblogs As CommunityServer.Blogs.Components.Weblogs
    Me._Blog = objCSWeblogs.GetWeblog(Me._ApplicationKey)
  End Sub

  Public Sub LoadBlog(ByVal XML As String)
    Dim Blog As New BlogMLBlog
    Try
      Blog = BlogMLSerializer.Deserialize(New StringReader(XML))
    Catch ex As Exception
      Throw New Exception("Couldn't load your BlogML file. Maybe it is wellformedness")
    End

    Try
      Dim Categories As Hashtable
      Categories = ReadCategories(Blog)

      LoadPosts(Blog, Categories)

      UpdateStats(Blog)
    End Sub

    Private Function ReadCategories(ByVal Blog As BlogMLBlog) As Hashtable
      Dim CategoriesHash As New Hashtable
      For Each Category As BlogMLCategory In Blog.Categories
        Dim NewCategory As New PostCategory With  NewCategory
          .DateCreated = Category.DateCreated
          .Description = Category.Description
          .IsEnabled = Category.Approved
          .Name = Category.Title
          .ParentID = 0
          .SectionID = Me._Blog.SectionID

        Dim objCSCats As PostCategories

        Try
          objCSCats.CreateCategory(NewCategory)
        Catch ex As Exception
          Throw New ArgumentException("Error when tried to add categories to database")
        End

        Try
          CategoriesHash.Add(Category.ID, Category.Title)
        End

        With Next Return CategoriesHash
        End Function

        Private Sub LoadPosts(ByVal Blog As BlogMLBlog, ByVal CategoryHash As Hashtable)
            Dim LastPostAuthor As String
            Dim LastPostAuthorID As Integer
            Dim LastPostDate As Date
            Dim LastPostName As String
            Dim LastPostSubject As String




            For Each Post As BlogMLPost In Blog.Posts
                Dim NewPost As New CommunityServer.Blogs.Components.WeblogPost
                Dim objCSPosts As CommunityServer.Blogs.Components.WeblogPosts

                With NewPost
                    .PostID = Post.ID
                    .Body = Post.Content.UncodedText
                    .BlogPostType = CommunityServer.Blogs.Components.BlogPostType.Post
                    .Subject = Post.Title
                    .ThreadDate = Post.DateCreated
                    .UserTime = Post.DateCreated
                    .PostDate = Post.DateCreated
                    .UserTime = Post.DateCreated
                    .SectionID = Me._Blog.SectionID
                    .SetExtendedAttribute("EverPublished", CType(Post.Approved, Boolean))
                    .IndexInThread = True
                    .IsApproved = True
                    .IsAggregated = True
                    .IsLocked = False
                    .PostConfig = CommunityServer.Blogs.Components.BlogPostConfig.IsAggregated

                End With
                'Add categories
                If Post.Categories.Count > 0 Then
                    Dim NewPostCats(Post.Categories.Count) As String
                    For i As Integer = 0 To Post.Categories.Count - 1
                        NewPostCats(i) = CategoryHash(Post.Categories(i).Ref)
                    Next
                    NewPost.Categories = NewPostCats
                End If

                'Add attachments
                'TO DO: Check to add attachments with checking the source code when RTM version has been released.
                'Currently we can't load post attachments

                objCSPosts.Add(NewPost)

                'Temporary saving stats
                LastPostAuthor = NewPost.Username
                LastPostAuthorID = NewPost.AuthorID
                LastPostDate = NewPost.PostDate
                LastPostName = NewPost.Name
                LastPostSubject = NewPost.Subject

                LoadComments(NewPost, Post)
                LoadTrackBacks(NewPost, Post)
            Next

            'Update blog stats
            Me._Blog.MostRecentPostAuthor = LastPostAuthor
            Me._Blog.MostRecentPostAuthorID = LastPostAuthorID
            Me._Blog.MostRecentPostDate = LastPostDate
            Me._Blog.MostRecentPostName = LastPostName
            Me._Blog.MostRecentPostSubject = LastPostSubject
        End Sub
        Private Sub LoadComments(ByVal NewPost As Post, ByVal Post As BlogMLPost)
            If Post.Comments.Count > 0 Then
                For Each Comment As BlogMLComment In Post.Comments
                    Dim NewComment As New CommunityServer.Blogs.Components.WeblogPost
                    Dim objCSComments As CommunityServer.Blogs.Components.WeblogPosts

                    With NewComment
                        .Body = Comment.Content.UncodedText
                        .BlogPostType = Blogs.Components.BlogPostType.Comment
                        .Subject = Comment.Title
                        .ThreadDate = Comment.DateCreated
                        .UserTime = Comment.DateCreated
                        .PostDate = Comment.DateCreated
                        .UserTime = Comment.DateCreated
                        .SectionID = Me._Blog.SectionID
                        .SetExtendedAttribute("EverPublished", True)
                        .SetExtendedAttribute("TitleUrl", Comment.UserUrl)
                        .SetExtendedAttribute("SubmittedUserName", Comment.UserName)
                        .IsApproved = CType(Comment.Approved, Boolean)
                        .ParentID = NewPost.PostID
                        .ThreadID = NewPost.ThreadID

                    End With

                    objCSComments.Add(NewComment)

                    'Update blog counter
                    Me._BlogCommentCount += 1
                Next
            End If
        End Sub

        Private Sub LoadTrackBacks(ByVal NewPost As Post, ByVal Post As BlogMLPost)
            If Post.Trackbacks.Count > 0 Then
                For Each TrackBack As BlogMLTrackback In Post.Trackbacks
                    Dim NewTrackBack As New Blogs.Components.WeblogPost
                    Dim objCSTrackBacks As Blogs.Components.WeblogPosts

                    With NewTrackBack
                        .Body = TrackBack.Title
                        .BlogPostType = Blogs.Components.BlogPostType.Trackback
                        .Subject = TrackBack.Title
                        .ThreadDate = TrackBack.DateCreated
                        .UserTime = TrackBack.DateCreated
                        .PostDate = TrackBack.DateCreated
                        .UserTime = TrackBack.DateCreated
                        .SectionID = Me._Blog.SectionID
                        .SetExtendedAttribute("EverPublished", True)
                        .SetExtendedAttribute("TitleUrl", TrackBack.Url)
                        .SetExtendedAttribute("trackbackName", "TrackBack")
                        .IsApproved = CType(TrackBack.Approved, Boolean)
                        .ParentID = NewPost.PostID
                        .ThreadID = NewPost.ThreadID

                    End With

                    objCSTrackBacks.Add(NewTrackBack)

                    'Update blog counter
                    Me._BlogTrackBackCount += 1
                Next
            End If
        End Sub
        Private Sub UpdateStats(ByVal Blog As BlogMLBlog)
            Me._Blog.PostCount += Blog.Posts.Count
            Me._Blog.CommentCount = Me._BlogCommentCount
            Me._Blog.TrackbackCount = Me._BlogTrackBackCount
        End Sub

    End Class

    Sub Page_Load(sender as Object, e as EventArgs)
    	Dim Path as String = "d:tmpBlogMLBlogML.xml"
    	Dim reader as New Reader("chris", Request.PhysicalApplicationPath)

    	If File.Exists(Path) Then
    		Dim sr as New StreamReader(File.Open(Path, FileMode.Open))
    		Dim xml as string = sr.ReadToEnd

    		reader.LoadBlog(xml)

    		Response.Write("Content moved successfully!")
    	Else
    		Response.Write("Uh-oh. Something crapped.")
    	End If

    End Sub

</script>
<html>
    <head>
    </head>
    <body>
        <form runat="server">
            <!-- Insert content here -->
        </form>
    </body>
</html>
```

I hacked up this file in WebMatrix and slapped it into the webroot of my new
CommunityServer install. This way I was able to copy the content to a local install before pushing the final product out into the wild, and I didn't have to recompile any of CS to get it working. Merci, Keyvan!
