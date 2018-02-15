---
layout: post
title: Raytracing Framework
date: 2018-02-13
categories: giclass
content-folder: /post-content/2018/02/13/raytracing-framework
---

<style type="text/css">
  .halfimg {
    display: inline-block;
    width: 50%;
  }
</style>

The basic raytracing framework has been implemented in this second assignment.
When the program launches, it's rendering the scene using OpenGL, and the user
can position the camera using the keyboard and mouse. To initiate the render,
the user taps the space bar. Once the render is complete, it's displayed on top
of the realtime render, and the user can tap space to toggle between the OpenGL
render and the raytraced render.

Here's the scene from the first post rendered using the raytracer:

<a href="{{page.content-folder}}/rendered_front.png">
  <img src="{{page.content-folder}}/rendered_front.png" />
</a>

Additionally, for extra credit, here are screenshots of the scene with an
alternative camera position, rendered both in real-time and with the raytracer.

<a class="halfimg" href="{{page.content-folder}}/realtime_alt.png">
  <img src="{{page.content-folder}}/realtime_alt.png" />
</a><a class="halfimg" href="{{page.content-folder}}/rendered_alt.png">
  <img src="{{page.content-folder}}/rendered_alt.png" />
</a>

