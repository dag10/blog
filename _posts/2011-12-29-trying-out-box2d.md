---
layout: post
title: Trying out Box2d
date: 2011-12-29
tags: [Box2D, c++, graphics, SFML]
photo-folder: /post_images/2011/12/29/trying-out-box2d
---

<div class="image-right">
  <img width="300" src="{{page.photo-folder}}/box2d-dominoes.png" />
  <em>Dominoes falling towards a house.</em>
</div>

What is Box2D? It’s a
[free and open source 2D physics engine](http://box2d.org/about). It is
developed with C++, and has fortunately been ported to many other languages,
including Actionscript and Java. I was eager to try it out.

At the same time, I was eager to get more familiar with the new
[C++11](http://en.wikipedia.org/wiki/C++11) standard I’ve been hearing about
(a.k.a. C++0x). So I made a small program to get a taste of Box2D and C++11
features. You can view and download the program
[here](https://github.com/dag10/sfml-box2d-demo/releases/tag/v1.0).

To use it, drag out a rectangle with your mouse. When you release the mouse,
the rectangle becomes a object in the world. It is affected by gravity, and
interacts realistically with other objects. If you happen to own a touch
screen, you can press space to hide the mouse cursor. You’re welcome.

Mixing Box2D with SFML graphics was a quite tricky. To keep track of the
objects, I created an std::vector of this struct:

<div class="code-leadin">
  <a href="https://github.com/dag10/sfml-box2d-demo/blob/f3238b80/include/Environment.h#L19">
    Environment.h:19
  </a> (rev f3238b80)
</div>
```cpp
typedef struct {
    shared_ptr graphic;
    shared_ptr body;
} PhysicsObject;
```

There was a problem though: The Box2D world’s coordinates are 1 unit = 1
meter, and the Y-axis increases upwards. SFML coordinates, however, are more
conventional computer graphics coordinates: 1 unit = 1 pixel, and the Y-axis
increased downwards. To add to these troubles, the SFML view (sf::view) has to
be able to scale (zoom) and move around the world.
<!-- more -->
To overcome this issue, I did two things. First, I made the Environment class
update an internal static sf::view during each render, representing what view
should be rendered to the window. However, I always keep the window’s view the
default view. The internal sf::view is only for the second thing I did: I made
two static functions in the Environment for translating world coordinates to
screen coordinates, and vice versa.

<div class="code-leadin">
  <a href="https://github.com/dag10/sfml-box2d-demo/blob/f3238b80/src/Environment.cpp#L113">
    Environment.cpp:113
  </a> (rev f3238b80)
</div>
```cpp
/*
 * Translate screen coordinates into world coordinates
 */
b2Vec2 Environment::ScreenToWorldPosition(b2Vec2 vec) {
    vec.x /= pixelsPerMeter;
    vec.y /= -pixelsPerMeter;
 
    vec.x -= (view.GetCenter().x + view.GetHalfSize().x);
    vec.y -= (-view.GetCenter().y + view.GetHalfSize().y);
 
    return vec;
}
 
/*
 * Translate world coordinates into screen coordinates
 */
b2Vec2 Environment::WorldToScreenPosition(b2Vec2 vec) {
    vec.x += (view.GetCenter().x + view.GetHalfSize().x);
    vec.y += (-view.GetCenter().y + view.GetHalfSize().y);
 
    vec.x *= pixelsPerMeter;
    vec.y *= -pixelsPerMeter;
 
    return vec;
}
```

With that, all I had to do to render them is iterate through all PhysicsObject
elements in the vector, update the scale of the sf::Shape, update the position
and rotation (while converting radians to degrees), and draw it to the
supplied sf::RenderTarget:

<div class="code-leadin">
  <a href="https://github.com/dag10/sfml-box2d-demo/blob/f3238b80/src/Environment.cpp#L67">
    Environment.cpp:67
  </a> (rev f3238b80)
</div>
```cpp
/* Render objects */
for (shared_ptr &obj : objects) {
  b2Vec2 pos = WorldToScreenPosition(obj->body->GetPosition());

  obj->graphic->SetScale(
    pixelsPerMeter * zoomFactor,
    pixelsPerMeter * zoomFactor);
  obj->graphic->SetPosition(pos.x, pos.y);
  obj->graphic->SetRotation(rad2deg(obj->body->GetAngle()));

  target.Draw(*obj->graphic);
}
```

And voilà!

As for C++11, I got a pretty nice taste of it. My favorite feature is the
[smart pointer](http://en.cppreference.com/w/cpp/memory/unique_ptr), which owns
and manages pointers and object instances. In particular,
[shared_ptr](http://en.cppreference.com/w/cpp/memory/shared_ptr) allows you to
easily set a custom destroy function in the form of a
[lambda](http://en.cppreference.com/w/cpp/language/lambda) — another C++11
feature I love. Here’s one line of my program that uses both of these features
nicely, and even uses [auto](http://en.cppreference.com/w/cpp/language/auto) —
another syntactical gift provided by the new standard):

<div class="code-leadin">
  <a href="https://github.com/dag10/sfml-box2d-demo/blob/f3238b80/src/Environment.cpp#L101">
    Environment.cpp:101
  </a> (rev f3238b80)
</div>
```cpp
// Will be automatically destroyed by world
auto body = shared_ptr(world->CreateBody(&blockDef),
     [this](b2Body *ptr) { world->DestroyBody(ptr); });
```

The line above creates a shared_ptr containing a b2Body — a rigid body in the
Box2D engine. It also sets and implements a custom destroy function. You can’t
simply delete a b2Body instance; you must pass it to the b2World’s DestroyBody
method instead. And that’s what this destroy function does. I can now continue
to write code worry-free, knowing that as soon as body is no longer in use,
the world will be asked to destroy it!

I’m might be misusing some smart pointers in my code. I’m still learning how to
appropriately use them.

The project is found [here](https://github.com/dag10/sfml-box2d-demo).

You can download a Windows binary
[here](https://github.com/dag10/sfml-box2d-demo/releases).

