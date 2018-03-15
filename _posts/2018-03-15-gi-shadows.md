---
layout: post
title: Phong Shading and Shadows
date: 2018-03-15
categories: giclass
content-folder: /post-content/2018/03/15/shadows
---

<style type="text/css">
  .halfimg {
    display: inline-block;
    width: 50%;
  }
</style>

For the third Global Illumination assignment, I implemented phong shading and
shadows from light sources. At this time I also made the two sphere separate
colors, seen in the left image below. The right image is the resulting
raytraced image.

<a class="halfimg" href="{{page.content-folder}}/phong_realtime.png">
  <img src="{{page.content-folder}}/phong_realtime.png" />
</a><a class="halfimg" href="{{page.content-folder}}/phong_one_light.png">
  <img src="{{page.content-folder}}/phong_one_light.png" />
</a>

And for extra credit, here's a render of the scene with two directional lights
instead of one. To keep the overall intensity of the lighting the same, the two
directional lights each have half the diffuse brightness as the previous single
light.

<a href="{{page.content-folder}}/phong_two_lights.png">
  <img src="{{page.content-folder}}/phong_two_lights.png" />
</a>

