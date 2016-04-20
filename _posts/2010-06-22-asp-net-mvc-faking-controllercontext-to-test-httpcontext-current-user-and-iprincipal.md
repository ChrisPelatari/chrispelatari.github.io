---
layout: post
title: ASP.NET MVC - Faking ControllerContext to test HttpContext.Current.User and IPrincipal
date: 2010-06-22 12:57
author: chrispelatari
comments: true
categories: [Uncategorized]
---

<p>This was pretty straightforward but I didn't find it written up anywhere on 
the web so here goes. What follows is how I addressed testing IPrincipal in 
ASP.NET MVC using <a href="http://xunit.codeplex.com/">xunit.net</a></p>
<p>Let's start with the test:</p><pre><span style="background-color:lightgrey;color:teal;">  1</span> [Fact]
<span style="background-color:lightgrey;color:teal;">  2</span> <span style="color:blue;">public</span> <span style="color:blue;">void</span> changes_password() {
<span style="background-color:lightgrey;color:teal;">  3</span>   <span style="color:green;">//arrange
</span><span style="background-color:lightgrey;color:teal;">  4</span>   <font color="#0000ff">var</font> controller = ObjectFactory.GetInstance&lt;AccountController&gt;();		
<span style="background-color:lightgrey;color:teal;">  5</span>   controller.ControllerContext = <span style="color:blue;">new</span> TestControllerContext();
<span style="background-color:lightgrey;color:teal;">  6</span> 
<span style="background-color:lightgrey;color:teal;">  7</span>   <span style="color:green;">//act
</span><span style="background-color:lightgrey;color:teal;">  8</span>   <font color="#0000ff">var</font> result = controller.ChangePassword(<span style="color:maroon;">"password"</span>, <span style="color:maroon;">"p455w0rd"</span>, <span style="color:maroon;">"p455w0rd"</span>);
<span style="background-color:lightgrey;color:teal;">  9</span> 
<span style="background-color:lightgrey;color:teal;"> 10</span>   <span style="color:green;">//assert
</span><span style="background-color:lightgrey;color:teal;"> 11</span>   <font color="#0000ff">var</font> viewResult = Assert.IsType&lt;RedirectToRouteResult&gt;(result);
<span style="background-color:lightgrey;color:teal;"> 12</span> }</pre>
<p>notice line 5. why are we setting a custom ControllerContext here? 
ControllerContext tells the current controller about things like HttpContext, 
which will be unavailable during tests (whoops!) This is needed because 
somewhere in the Action code, I am making a call into <font style="background-color:#ffff00;" color="#999999">User.Identity.Name</font>, which 
is supplied by HttpContext at runtime. Again, since this isn't available during 
testing, I have to tell the controller how to find the fake httpcontext used 
then.</p>
<p>For this project, I'm using simple hand-rolled stubs. Here is the code for 
TestControllerContext:</p><pre><span style="background-color:lightgrey;color:teal;">  1</span> 	<span style="color:blue;">public</span> <span style="color:blue;">class</span> TestControllerContext : ControllerContext {
<span style="background-color:lightgrey;color:teal;">  2</span> 		<span style="color:blue;">public</span> <span style="color:blue;">override</span> System.Web.HttpContextBase HttpContext {
<span style="background-color:lightgrey;color:teal;">  3</span> 			<span style="color:blue;">get</span> {
<span style="background-color:lightgrey;color:teal;">  4</span> 				<span style="color:blue;">return</span> <span style="color:blue;">new</span> TestHttpContext();
<span style="background-color:lightgrey;color:teal;">  5</span> 			}
<span style="background-color:lightgrey;color:teal;">  6</span> 			<span style="color:blue;">set</span> {
<span style="background-color:lightgrey;color:teal;">  7</span> 				<span style="color:blue;">base</span>.HttpContext = value;
<span style="background-color:lightgrey;color:teal;">  8</span> 			}
<span style="background-color:lightgrey;color:teal;">  9</span> 		}
<span style="background-color:lightgrey;color:teal;"> 10</span> 	}</pre>
<p>instead of returning the runtime HttpContext (which doesn't exist, remember) 
I'm supplying another hand-rolled stub. Here is that code:</p><pre><span style="background-color:lightgrey;color:teal;">  1</span> 	<span style="color:blue;">public</span> <span style="color:blue;">class</span> TestHttpContext : HttpContextBase {
<span style="background-color:lightgrey;color:teal;">  2</span> 		<span style="color:blue;">public</span> <span style="color:blue;">override</span> System.Security.Principal.IPrincipal User {
<span style="background-color:lightgrey;color:teal;">  3</span> 			<span style="color:blue;">get</span> {
<span style="background-color:lightgrey;color:teal;">  4</span> 				<span style="color:blue;">return</span> <span style="color:blue;">new</span> TestPrincipal();
<span style="background-color:lightgrey;color:teal;">  5</span> 			}
<span style="background-color:lightgrey;color:teal;">  6</span> 			<span style="color:blue;">set</span> {
<span style="background-color:lightgrey;color:teal;">  7</span> 				<span style="color:blue;">base</span>.User = value;
<span style="background-color:lightgrey;color:teal;">  8</span> 			}
<span style="background-color:lightgrey;color:teal;">  9</span> 		}
<span style="background-color:lightgrey;color:teal;"> 10</span> 	}</pre>
<p>again, same principal :) because I'm concerned about calling into User for 
the Identity.Name property, I return another stub that implements IPrincipal. 
Here is that code:</p><pre><span style="background-color:lightgrey;color:teal;">  1</span> 	<span style="color:blue;">public</span> <span style="color:blue;">class</span> TestPrincipal : IPrincipal{
<span style="background-color:lightgrey;color:teal;">  2</span> 		<span style="color:blue;">public</span> IIdentity Identity {
<span style="background-color:lightgrey;color:teal;">  3</span> 			<span style="color:blue;">get</span> { <span style="color:blue;">return</span> <span style="color:blue;">new</span> GenericIdentity(<span style="color:maroon;">"you@me.com"</span>); }
<span style="background-color:lightgrey;color:teal;">  4</span> 		}
<span style="background-color:lightgrey;color:teal;">  5</span> 
<span style="background-color:lightgrey;color:teal;">  6</span> 		<span style="color:blue;">public</span> <span style="color:blue;">bool</span> IsInRole(<span style="color:blue;">string</span> role) {
<span style="background-color:lightgrey;color:teal;">  7</span> 			<span style="color:blue;">throw</span> <span style="color:blue;">new</span> NotImplementedException();
<span style="background-color:lightgrey;color:teal;">  8</span> 		}
<span style="background-color:lightgrey;color:teal;">  9</span> 	}</pre>
<p>now, when the controller code that was calling User.Identity.Name is tested, 
it will return the name <a href="mailto:you@me.com">you@me.com</a>. Line 11 of 
the test code above asserts the test passes because if an error occurred, I 
would redisplay the form with errors shown using the View() method. A redirect 
says that the change password op worked:</p><pre><span style="background-color:lightgrey;color:teal;">  1</span> <span style="color:blue;">if</span> (MembershipService.ChangePassword(User.Identity.Name, currentPassword, newPassword)) 
<span style="background-color:lightgrey;color:teal;">  2</span>   <span style="color:blue;">return</span> RedirectToAction(<span style="color:maroon;">"ChangePasswordSuccess"</span>);</pre>
<p>hth.</p>
