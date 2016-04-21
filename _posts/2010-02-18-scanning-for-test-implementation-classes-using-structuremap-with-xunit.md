---
layout: post
title: Scanning for Test implementation classes using StructureMap with xunit
date: 2010-02-18 07:59
author: chrispelatari
comments: true
categories: [Uncategorized]
---

I have an [xunit test project](http://xunit.codeplex.com/) that is using hand-rolled stubs as concrete implementations of interfaces.
[StructureMap](http://structuremap.sourceforge.net/Default.htm) is
the DI container I'm using. I was looking at the names of my stubs, and they
followed the convention of TestXYZ as the concrete implementation of IXYZ.

To use [StructureMap](http://structuremap.sourceforge.net/Default.htm) from [xunit tests](http://xunit.codeplex.com/), I created a base
class for any fact class that wanted to use ObjectFactory. In the base class
ctor, I call the bootstrapper's ConfigureStructureMap method.

At first I just had a bunch of
x.ForRequestedType<IXYZ>().TheDefaultIsConcreteType<TestXYZ>();
because I had only a handful of stubs and I didn't quite grasp how to scan like
the default scanner, only adding "Test" to the beginning of the class name.

Then I found the [secret sauce over here](http://www.bjoernrochel.de/2009/07/24/cutting-the-fluff-from-service-registration-or-how-to-do-funky-stuff-with-coc-castledynamicproxy-structuremap/), via a method called FindPluginType.

Here is my bootstrapper code for my [xunit test project](http://xunit.codeplex.com/):

```csharp
public class TestScanner : ITypeScanner{
  public void Process(Type type, PluginGraph graph) {
    if(type.Name.StartsWith("Test")){
      var pluginType = FindPluginType(type);
      if(pluginType == null)
        return;

      graph.AddType(pluginType, type);
    }				
  }

  static Type FindPluginType(Type concreteType) {
    var interfaceName = "I" + concreteType.Name.Replace("Test", "");
    return concreteType.GetInterfaces().Where(t => string.Equals(t.Name, interfaceName, StringComparison.Ordinal)).FirstOrDefault();
  }
}

public static class Bootstrapper {
  public static void ConfigureStructureMap() {
    ObjectFactory.Initialize(x =>
      {
        x.Scan(s =>
          {
            s.TheCallingAssembly();
            s.WithDefaultConventions();
            s.With<TestScanner>();
  				});
  			});
      }
}
```

What
results is essentially the [DefaultConventionScanner](http://structuremap.sourceforge.net/ScanningAssemblies.htm#section9),
only it's looking for TestXYZ as the concrete implementation of IXYZ.

Killer.
