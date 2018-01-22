---
layout: post
title: Setting The Scene
date: 2018-01-21
categories: giclass
content-folder: /post-content/2018/01/21/gi-setting-the-scene
---

To create and preview the geometry layout for my Global Illumination scene,
I branched my toy OpenGL engine and created a scene. The source code for the
scene is on my GitHub in
[LayoutScene.cpp](https://github.com/dag10/DrewGraphics/blob/giclasslayout/src/scenes/LayoutScene.cpp).

Here's the output from the camera's perspective:

<a href="{{page.content-folder}}/screenshot.png">
  <img src="{{page.content-folder}}/screenshot.png" />
</a>

The coordinate system is right-handed, so the forward vector is `(0, 0, -1)`.

The floor grid is a 12 x 28 unit grid.

The camera is positioned at the position `(-3, 2, 5)`, with its forward vector
being `(0, -0.164, 0)`. Its vertical field of view is 60 degrees.

Both spheres are 2.5 units in diameter.

The sphere closest to the camera, which will become the transparent sphere
in the ray tracer, is at position `(-3, 2, 0)`.

The sphere behind it, which will become the reflective sphere, is positioned
at `(-1, 1.5, -2)`.

The lighting in the scene is a directional light, pointing in the direction
of `(0, -1, -0.3)` normalized.

Here's a top-down orthographic projection:

<a href="{{page.content-folder}}/ortho.png">
  <img src="{{page.content-folder}}/ortho.png" />
</a>

