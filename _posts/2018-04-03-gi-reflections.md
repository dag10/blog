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
  .right {
    float: right;
  }
</style>

The fifth assignment is adding reflections using recursive ray tracing. I added
a *reflectance* property to each material, which ranges from 0.0 to 1.0. The
local illumination (phong) is blended with the results of ray tracing the
reflected ray based on this value.

Here's a screenshot of the scene with the far sphere being 100% reflective,
the floor being 10% reflective, and the background being changed to blue.

<a href="{{page.content-folder}}/reflections_additive.png">
  <img src="{{page.content-folder}}/reflections_additive.png" />
</a>

I made the materials able to be reflective in two different modes of blending:
weighted, and additive. With weighted blending, the final color of the material
surface is

```
((1 - reflectance) * localShadedColor) +
(reflectance * reflectionShadedColor)
```

whereas with additive reflection blending, the final color is

```
localShadedColor + (reflectance * reflectionShadedColor);
```

<a class="halfimg right" href="{{page.content-folder}}/reflections_additive_preview.png">
  <img src="{{page.content-folder}}/reflections_additive_preview.png" />
</a>

To make the far sphere look more like a shiny metal sphere, it's not just 100%
reflective, it's additively reflective. Its reflection is blended additively
with a phong shading that has a 100% white specular color and a 10% white
diffuse color. As a result, the image to the right is what the OpenGL preview
looks like.

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

