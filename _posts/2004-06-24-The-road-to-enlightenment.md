---
layout: post
title: The road to enlightenment
---
<p>Earlier this year I started using NUnit to see what all the fuss was about. I 
started on a subset of an application that I'm working on, using it for the 
database interaction code. I figured that would be a good place to start, since 
I'm not sure how to test UI stuff, and these were the parts handed to me when 
the application was in spec stage.</p>
<p>I took a pretty simplistic (and probably wrong by some accounts) approach - 
set up a database with the same structure as what would be used in the end 
(appended with NUnit to separate the DBs) and make my assertions on the objects 
returned or modified there.</p>
<p>So, at the suggestion of <a href="http://weblogs.asp.net/DatagridGirl">someone who digs DataGrids</a>, I 
picked up the TDD in MSFT.NET book by Newkirk &amp;Vorontsov. I just barely 
cracked chapter 2 and came across something that I did not know and did not 
occur to me thru running my tests (with my apologies):</p>
<blockquote dir="ltr" style="MARGIN-RIGHT: 0px">
  <p>The function <em>Init</em> is marked with an attribute called 
  [<em>SetUp</em>]. NUnit uses this attribute to ensure that this method is 
  called prior to each test being run, which means that each test method gets a 
  newly created <em>Stack</em>, instead of one modified from a previous 
test.</p></blockquote>
<p dir="ltr">Seriously? I just figured that [<em>SetUp</em>] ran once, so all I 
did was initialize my connection string there. This book is already pretty good, 
if I'm able to learn something by chapter 2...I'm looking forward to finishing 
it :)</p>