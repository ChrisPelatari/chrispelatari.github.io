---
layout: post
title: Got an importer.
---
I have a project that requires that I convert a flat FoxPro Database to a 'normalized' Sql Server database. So far, I've gotten the foxpro data into SqlServer.

Today I created an Importer utility class to generate the proper data from flat-> normal database. Now I just need to create the logic that will migrate the data from one to the other... I've gotten as far as creating the datacontainers and filling the initial data from the original flat database into memory.

Also, I learned that you can have two different Main() methods in a solution, which one gets used depends on which one is selected as the startup project.  