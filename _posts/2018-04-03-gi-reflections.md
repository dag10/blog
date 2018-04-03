---
layout: post
title: Reflections
date: 2018-04-03
categories: giclass
content-folder: /post-content/2018/04/03/reflections
---

<style type="text/css">
  .halfimg {
    display: inline-block;
    width: 50%;
  }
</style>

The fifth assignment is adding reflections using recursive ray tracing. I added
a *reflectance* property to each material, which ranges from 0.0 to 1.0. The
local illumination (phong) is mixed with the results of ray tracing the
reflected ray based on this value.

Here's a screenshot of the scene with the near sphere being 10% reflective and
the back sphere being 100% reflective.

<a href="{{page.content-folder}}/reflections.png">
  <img src="{{page.content-folder}}/reflections.png" />
</a>

And here's two additional images that are fun to look at. The first is a
close-up of the red and green spheres, each being 70% reflective.

The second image shows my raytraced reflections not quite working. But it
looks pretty damn cool, right? Click it for the full-res screenshot, it's worth
it.

<a class="halfimg" href="{{page.content-folder}}/both_reflective.png">
  <img src="{{page.content-folder}}/both_reflective.png" />
</a><a class="halfimg" href="{{page.content-folder}}/oh_my.png">
  <img src="{{page.content-folder}}/oh_my.png" />
</a>

