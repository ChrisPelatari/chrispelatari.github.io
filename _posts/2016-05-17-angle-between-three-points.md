---
title: "angle between three points"
layout: post
author: chrispelatari
categories: [ruby,math]
---

### This was a task I had to complete to attempt to find a right angle from 3 cartesian coordinates, +/- 5 degrees.

Of course the first place I looked was [StackOverflow](http://stackoverflow.com/questions/1211212/how-to-calculate-an-angle-from-three-points) which led me to [this explanation](http://phrogz.net/angle-between-three-points) with some ruby code:

```ruby
def angle_between_points(p0, p1, p2)
  a = (p1[0]-p0[0])**2 + (p1[1]-p0[1])**2
  b = (p1[0]-p2[0])**2 + (p1[1]-p2[1])**2
  c = (p2[0]-p0[0])**2 + (p2[1]-p0[1])**2
  Math.acos( (a+b-c) / Math.sqrt(4*a*b) ) * 180/Math::PI
end
```

For my purposes, I simply created the three arrays and passed them to the method after a call to puts:

```ruby
p0 = [2005000,992453]
p1 = [1895297,949433]
p2 = [1920079,884362]

puts angle_between_points p0, p1, p2
```

Now, I can adjust the numbers in the .rb file and call it at the command line:

```
chris@IO  ~/Documents/code
$ ruby angle_between_points.rb
90.56350243137959
```
