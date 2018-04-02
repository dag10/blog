---
layout: post
title: Procedural Textures
date: 2018-04-02
categories: giclass
content-folder: /post-content/2018/04/02/procedural-textures
---

<style type="text/css">
  .halfimg {
    display: inline-block;
    width: 50%;
  }
</style>

The fourth Global Illumination assignment introduces UV mapping for procedural
texture generation or texture mapping. To achieve this, I added UVs to
spherical meshes and used barycentric interpolation to interpolate normals
and texture coordinates for all meshes–including the ground plane.

Here is the raytraced image with the diffuse checkerboard ground plane.

<a href="{{page.content-folder}}/uv_raytraced.png">
  <img src="{{page.content-folder}}/uv_raytraced.png" />
</a>

