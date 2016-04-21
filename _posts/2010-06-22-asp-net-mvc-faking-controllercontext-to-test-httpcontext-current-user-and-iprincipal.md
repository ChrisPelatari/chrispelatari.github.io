---
layout: post
title: ASP.NET MVC - Faking ControllerContext to test HttpContext.Current.User and IPrincipal
date: 2010-06-22 12:57
author: chrispelatari
comments: true
categories: [aspnet,xunit,mvc]
---

This was pretty straightforward but I didn't find it written up anywhere on
the web so here goes. What follows is how I addressed testing IPrincipal in
ASP.NET MVC using [xunit.net](http://xunit.codeplex.com/)

Let's start with the test:

```csharp
[Fact]
public void changes_password() {
  //arrange
  var controller = ObjectFactory.GetInstance<AccountController>();
  controller.ControllerContext = new TestControllerContext();
  //act
  var result = controller.ChangePassword("password", "p455w0rd", "p455w0rd");
  //assert
  var viewResult = Assert.IsType<RedirectToRouteResult>(result);
  }
```

notice line 5. why are we setting a custom ControllerContext here?
ControllerContext tells the current controller about things like HttpContext,
which will be unavailable during tests (whoops!) This is needed because
somewhere in the Action code, I am making a call into User.Identity.Name, which
is supplied by HttpContext at runtime. Again, since this isn't available during
testing, I have to tell the controller how to find the fake httpcontext used
then.

For this project, I'm using simple hand-rolled stubs. Here is the code for
TestControllerContext:

```csharp
public class TestControllerContext : ControllerContext {
  public override System.Web.HttpContextBase HttpContext {
    get {
      return new TestHttpContext();
    }
    set {
      base.HttpContext = value;
    }
  }
}
```

instead of returning the runtime HttpContext (which doesn't exist, remember)
I'm supplying another hand-rolled stub. Here is that code:

```csharp
public class TestHttpContext : HttpContextBase {
  public override System.Security.Principal.IPrincipal User {
    get {
      return new TestPrincipal();
    }
    set {
      base.User = value;
    }
  }
}
```

again, same principal :) because I'm concerned about calling into User for
the Identity.Name property, I return another stub that implements IPrincipal.
Here is that code:

```csharp
public class TestPrincipal : IPrincipal{
  public IIdentity Identity {
    get { return new GenericIdentity("you@me.com"); }
  }
  public bool IsInRole(string role) {
    throw new NotImplementedException();
  }
}
```

now, when the controller code that was calling User.Identity.Name is tested,
it will return the name you@me.com. Line 11 of
the test code above asserts the test passes because if an error occurred, I
would redisplay the form with errors shown using the View() method. A redirect
says that the change password op worked:

```csharp
if (MembershipService.ChangePassword(User.Identity.Name, currentPassword, newPassword))
  return RedirectToAction("ChangePasswordSuccess");
```

hth.
