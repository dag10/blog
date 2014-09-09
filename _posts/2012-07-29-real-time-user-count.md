---
layout: post
title: Real-time User Count Without Any Javascript
date: 2012-07-29
tags: [graphics, mjpeg, node.js, real-time]
---

<div class="image-left">
  <img src="http://drewgottlieb.net:9192/online.png" />
  <em>Live Demonstration</em>
</div>

IP cameras are frequently streamed as
[M-JPEG](http://en.wikipedia.org/wiki/Motion_JPEG#M-JPEG_over_HTTP) over HTTP
connections. Why not use the same principle for other uses, too? Although
M-JPEG streaming doesn’t work in Internet Explorer, it can still be useful.

The underlying protocol is simply a multipart HTTP request using the
[x-mixed-replace](http://en.wikipedia.org/wiki/MIME#Mixed-Replace)
content type. Basically, the server sends the document (or in this case, image)
multiple times, with each part replacing the previous part. So when an IP
camera is streaming, it’s just sending multiple jpeg images that each replace
the previous image.

It looks like this:

```
HTTP/1.1 200 Ok
Content-Type: multipart/x-mixed-replace; boundary=--icecream

--icecream
Content-Type: image/jpeg
Content-Length: [length]

[data]

--icecream
Content-Type: image/jpeg
Content-Length: [length]

[data]

--icecream
```

(and so on)
<!-- more -->
In this bare-bones example, the boundary is *icecream*, but ideally you’d want
to use something that won’t appear in the data itself. Also, the content-type
can be anything, such as image/png.

While learning about this, a practical application immediately came to mind: a
real time online-users counter — such as the one above. This method is great
for this use because it fills two roles. First, it keeps a persistent
connection between the client and server, so we know when a user connects and
when that user disconnects. Second, it can display the user count in real-time
without requiring any page updates. This system can be used in places where
Javascript is not an option, such as on a forum.

I made it using [Node.js](http://nodejs.org), with
[Backbone.js](http://backbonejs.org), and
[node-canvas](https://github.com/learnboost/node-canvas/) — which unfortunately
does not work on Windows. If you’re familiar with Backbone, the code should be
rather self-explanatory.

[Here is the source](https://gist.github.com/dag10/48e6d25415ca92318815).

I can see some neat uses for this type of image, since content can be made
interactive without the use of client-side scripts. Interactivity can be
introduced by having links with the server returning *HTTP 204* No Content,
such as [this link](http://httpstat.us/204) (provided by
[httpstat.us](http://httpstat.us)). The client won’t go to a new page, but the
server will be aware of the client’s request and can perform an action. With
this, real-time tic-tac-toe or even hang-man is possible.

Just some thoughts.

You can follow discussion of this post on
[Hacker News](https://news.ycombinator.com/item?id=4307126).

------

**(03:28 EST) Update:** Through experimentation, I just discovered that
unfortunately, it is not possible to combine HTTP 204 links with image
streams, as I suggested in my last paragraph. Upon clicking any link, the
browser stops loading all resources, including streams. This is before it even
knows that the result status will be 204. What a bummer.

