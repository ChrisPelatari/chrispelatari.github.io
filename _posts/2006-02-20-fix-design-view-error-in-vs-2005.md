---
layout: post
title: FIX&#58; Design View error in VS 2005
date: 2006-02-20 19:20
author: chrispelatari
comments: true
categories: [professional_geek]
---

<p><a href="http://support.microsoft.com/kb/912019/en-us">Here's a link to the
hotfix </a>for the winforms designer error that looks like this:</p>
<blockquote style="margin-right:0;">
  <p><font face="Verdana" color="#ff0000" size="2">One or more errors encountered
  while loading the designer. The errors are listed below. Some errors can be
  fixed by rebuilding your project, while others may require code changes.
  TypeLoad failure. Unable to load one or more of the requested types. Retrieve
  the LoaderExceptions property for more information. <br /><br />at
  System.Reflection.Module.GetTypesInternal(StackCrawlMark&amp; stackMark)
  <br />at System.Reflection.Assembly.GetTypes() <br />at
  Microsoft.VisualStudio.Shell.Design.AssemblyObsoleteEventArgs..ctor(Assembly
  assembly) <br />at
  Microsoft.VisualStudio.Design.VSDynamicTypeService.ReloadAssemblyIfChanged(String
  codeBase) <br />at
  Microsoft.VisualStudio.Design.VSDynamicTypeService.CreateDynamicAssembly(String
  codeBase) <br />at
  Microsoft.VisualStudio.Design.VSTypeResolutionService.AssemblyEntry.get_Assembly()
  <br />at
  Microsoft.VisualStudio.Design.VSTypeResolutionService.AssemblyEntry.Search(String
  fullName, String typeName, Boolean ignoreTypeCase, Assembly&amp; assembly,
  String description) <br />at
  Microsoft.VisualStudio.Design.VSTypeResolutionService.SearchProjectEntries(AssemblyName
  assemblyName, String typeName, Boolean ignoreTypeCase, Assembly&amp; assembly)
  <br />at Microsoft.VisualStudio.Design.VSTypeResolutionService.GetType(String
  typeName, Boolean throwOnError, Boolean ignoreCase, ReferenceType refType)
  <br />at
  Microsoft.VisualStudio.Design.Serialization.CodeDom.AggregateTypeResolutionService.GetType(String
  name, Boolean throwOnError, Boolean ignoreCase) <br />at
  Microsoft.VisualStudio.Design.Serialization.CodeDom.AggregateTypeResolutionService.GetType(String
  name, Boolean throwOnError) <br />at
  System.ComponentModel.Design.Serialization.CodeDomSerializerBase.GetType(ITypeResolutionService
  trs, String name, Dictionary`2 names) <br />at
  System.ComponentModel.Design.Serialization.CodeDomSerializerBase.FillStatementTable(IDesignerSerializationManager
  manager, IDictionary table, Dictionary`2 names, CodeStatementCollection
  statements, String className) <br />at
  System.ComponentModel.Design.Serialization.TypeCodeDomSerializer.Deserialize(IDesignerSerializationManager
  manager, CodeTypeDeclaration declaration) <br />at
  System.ComponentModel.Design.Serialization.CodeDomDesignerLoader.PerformLoad(IDesignerSerializationManager
  manager) <br />at
  Microsoft.VisualStudio.Design.Serialization.CodeDom.VSCodeDomDesignerLoader.PerformLoad(IDesignerSerializationManager
  serializationManager) <br />at
  Microsoft.VisualStudio.Design.Serialization.CodeDom.VSCodeDomDesignerLoader.DeferredLoadHandler.Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferDataEvents.OnLoadCompleted(Int32
  fReload)</font></p></blockquote>
