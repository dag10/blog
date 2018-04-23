---
layout: post
title: Transmission
date: 2018-04-17
categories: giclass
content-folder: /post-content/2018/04/17/transmission
---

<style type="text/css">
  .halfimg {
    display: inline-block;
    width: 50%;
  }
  .right {
    float: right;
  }
</style>

Similarly to the previous assignment, the sixth assignment introduces rendering
of transmissive surfaces, taking refraction into account. Continuing with the
theme of recreating J. Turner Whitted's test scene with a reflective and
transmissive sphere, I've made the front sphere of my scene be transmissive.

Here's the render, using the blue sky background:

<a href="{{page.content-folder}}/refraction.png">
  <img src="{{page.content-folder}}/refraction.png" />
</a>

And to better illustrate the refraction, here's a render with the background
pixels being the ray's final direction vector coded as color:

<a href="{{page.content-folder}}/refraction_normals.png">
  <img src="{{page.content-folder}}/refraction_normals.png" />
</a>

<a class="halfimg right" href="{{page.content-folder}}/oops.png">
  <img src="{{page.content-folder}}/oops.png" />
</a>

And just like last time, here's a fun blooper render, where the ray was entering
the sphere but never leaving, just bouncing off its inner surfaces until it
hit the maximum number of bounces.
