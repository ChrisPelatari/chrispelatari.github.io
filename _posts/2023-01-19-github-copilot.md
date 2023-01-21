---
title: "GitHub CoPilot"
layout: post
author: chrispelatari
categories: [GitHub, AI]
---

## I was using [GitHub CoPilot](https://docs.github.com/en/copilot) and ran into a perfect example of keystrokes saved when writing boilerplate code. 

First, I created a list [here](/categories-list/) with jekyll and copied that list into a DbContext class that I wanted that seed data added to. As I was typing the first model data, copilot guessed what I wanted was from the pasted list so it was a bunch of TAB/ENTER and that boilerplate code was done without me having to fill in the blanks myself.

`dotnet ef migrations add SeedCategoryData`

and 

`dotnet ef database update`

picked all of this up and created the seed data in the database. This is barely scratching the surface of how this thing could be useful. That's pretty cool.