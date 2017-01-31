---
layout: post
title: Mixing Reality with Virtual Reality
date: 2017-01-31
tags: [hololens, vive, mixed reality, virtual reality]
content-folder: /post-content/2017/01/31/mixing-reality-with-vr
---

Virtual reality is a pretty magical experience when it comes to making art.
However, if you have friends in the room watching you, the magic is lost on
them. They can only see the experience by looking at a distorted preview of the
player’s perspective on a computer monitor.
 
A friend was recently painting a 3D submarine in Tilt Brush. “Look at this
periscope!” she said. I told her to look closer at it, and I leaned into my
computer monitor to get a glimpse of what she made.
 
We can do better than this. Why do I have to get up off the couch to see what
my friend is creating? Why can’t I just lean back and see the art floating in
the middle of the room?
 
Until recently, such magic would have been impossible. That is, until Microsoft
released development kits of their new mixed-reality HoloLens glasses. I’m
fortunate to have access a couple units, and I really wanted to use mixed
reality to share in a VR experience.
 
So I spent a week making a proof of concept to feel that out. It runs on the
HTC Vive, a VR system that includes two positionally-tracked controllers.
Here’s what that looks like:

<iframe width="560" height="315" src="//www.youtube-nocookie.com/embed/XPYb2IsZL68" frameborder="0" allowfullscreen>
</iframe>
<!-- more -->

I didn’t want to spend a lot of time recreating a 3D painting app like Tilt
Brush, so I threw together an app in which the VR player uses their controller
to draw cubes in the air. Simple stuff, since that’s not the interesting part.
 
The interesting part is that when the same app runs on a HoloLens, it
automatically connects to the VR session using Unity’s built-in networking and
matchmaking service.
 
A challenge in this experiment was not just getting the Vive and HoloLens to
talk to each other, but to bring them to a shared understanding of space. How
do we align the virtual and room spaces? Ideally this would happen
automatically, but I couldn’t think of a way to do this just using the
technology offered by the Vive and HoloLens. Perhaps you could attach tracking
symbols to the VR base stations? I only had four days to work on this before
flying away for several months, so I went with a different, quicker solution.
When the HoloLens app connects to the VR app, the game enters “alignment mode”.
The HoloLens speaks, prompting the wearer to pick up one of the Vive controllers
and intersect it with a floating ‘ghost’ controller. Once the real and
holographic controllers are aligned, the wearer pulls the trigger and the voice
proudly announces, “You are now aligned.” There’s no limit on how many people
can join in, and I successfully tested with two HoloLenses participating in the
same session.

This quick and dirty solution works better than expected! There are four degrees
of alignment: three degrees of position, and one degree of rotation around the
room’s vertical axis. The biggest error comes from slight inaccuracy in rotation
when aligning the controller. If just one degree off, one won’t really notice
much misalignment near where the alignment point was, but they’ll see increasing
misalignment as they move farther away from that point. In the future I can
reduce this degree of error by prompting the alignment of three points instead
of just one, and using the position information from these to determine
rotation, ignoring the controller’s actual rotation at each point.

Let’s talk about the experience. There are two interesting takeaways from this
kind of setup.
 
First, you can just forget about the VR headset! Just put it down, don the
HoloLens, grab the controllers, and get to making art – floating in the middle
of your actual living room, not from some mysterious black void.

<img src="{{page.content-folder}}/ar_blocks.gif" />

Second, people can collaborate in within the same space, across virtual and
holographic environments. As a spectator with a HoloLens, you can say to the
VR player “I have an idea, hand me a controller” and then interact with the art
yourself. Or if you’re ignoring the VR headset entirely and just interacting as
two people wearing HoloLenses, each of you can take one controller and you can
build very large shapes – with some communication.

<img src="{{page.content-folder}}/ar_collaboration.gif" />

I have no doubt this kind of mixed space will be a big part of the future,
especially for creative industries. As virtual and mixed reality become
stronger platforms for content creation, it’s only inevitable that they’ll be
able to be interact on a whim.

If you have a Vive and a HoloLens, feel free to try the project out for
yourself! Get the source code from GitHub:
[https://github.com/dag10/HoloViveObserver](https://github.com/dag10/HoloViveObserver)

---

<em>Disclaimer: One week ago I started an internship at Google working on
[Tilt Brush](https://tiltbrush.com). This project was my own work from before
the internship and has no association with Google.</em>



