---
layout: post
title: Unable to find the requested .Net Framework Data Provider.  It may not be installed.
date: 2010-04-06 11:20
author: chrispelatari
comments: true
categories: [dotnet,SQLite]
---
```xml
<system.data>
  <DbProviderFactories>
      <remove invariant="System.Data.SQLite"/>
      <add name="SQLite Data Provider"
        invariant="System.Data.SQLite"
        description=".Net Framework Data Provider for SQLite"
        type="System.Data.SQLite.SQLiteFactory, System.Data.SQLite" />
  </DbProviderFactories>
</system.data>
```

this happened to me using subsonic on an x64 machine. adding the x64 binary
to /bin and adding the above to my web.config got me sorted.
