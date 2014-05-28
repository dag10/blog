---
layout: post
title: Storing Digital Data on an Audio Cassette
date: 2011-09-18
tags: [audio, cassette, data, data storage, fsk, rtty]
content-folder: /post-content/2011/09/18/storing-data-on-audio-cassette
---

<div class="image-left" style="width: 250px;">
  <img src="{{page.content-folder}}/overview.jpg" />
  <em>The cassette recorder hooked up to my computer's front audio ports.</em>
</div>

A few days ago my dad bought a simple audio cassette player/recorder to make a
digital copy of an old tape recording he had of Pioneer 10 leaving the solar
system. I had the opportunity to try something I always wanted to try: Storing
data on an audio cassette. After some researching, I decided to use
[RTTY](http://en.wikipedia.org/wiki/Radioteletype) (Radioteletype). I found an
awesome program called Digital Master 780, which is part of a freeware Ham
Radio software package,
[Ham Radio Deluxe](https://web.archive.org/web/20120720063807/http://wiki.ham-radio-deluxe.com/index.php?title=Main_Page).

To connect the tape player, I needed to use two 3.5mm
[TRS](http://en.wikipedia.org/wiki/TRS_connector) cables, one for my computer
to hear the cassette player’s output, and another one to send audio to the
player’s audio input for recording.

<div class="image-right" style="width: 200px;">
  <img src="{{page.content-folder}}/splice.jpg" />
  <em>My DIY 3.5mm TRS cable from two earphone cables.</em>
</div>

Since I only own one cable, I made a second one by using two old earphone
wires, wire strippers, two alligator clips, and tape. It looks messy, but it
[gets the job done]({{page.content-folder}}/splice_closeup.jpg)!

For reading and writing digital data to the tape, I tried out several audio
formats that the program could use. Due to the low audio quality that the tape
can store, I was only able to get away with using RTTY. After further
experimentation, I decided that these are the best settings I can use:

        100 Baud, 170 Hz shift, 7 bits (ASCII), 2 stop bits.

Success! Here’s a video of me writing two paragraphs of “Lorem ispum” text to
the tape:

<!-- more -->
<iframe width="560" height="315" src="//www.youtube-nocookie.com/embed/BMVO4X5u-gE?rel=0" frameborder="0" allowfullscreen>
</iframe>

And here's a video of me reading the data back:

<iframe width="560" height="315" src="//www.youtube-nocookie.com/embed/EfcOOFiPw4w?rel=0" frameborder="0" allowfullscreen>
</iframe>

And here’s the [audio]({{page.content-folder}}/sample.ogg) if want to know what it
sounds like, or even decode it yourself: 
<iframe width="100%" height="120" scrolling="no" frameborder="no" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/23632022&amp;color=ff5500&amp;auto_play=false&amp;hide_related=false&amp;show_artwork=true">
</iframe>

Although slow, I just *had* to try storing a file on it. I took a low-quality
70-70 pixel .gif image and used this
[online tool](http://www.motobit.com/util/base64-decoder-encoder.asp) to
convert it into copyable Base64-encoded text. It took about ten minutes for it
to write the data to the cassette, and it used up half of the tape! After a
ten-minute reading of the tape, I was able to use the same website to convert
the Base64-encoded file back into its original form. It worked!

So what can I conclude about storing data on an audio cassette? It’s possible,
but it’s extremely slow and space-consuming. If anything, it’s only good for
storing text, as even the smallest files will consume half of your tape if
you’re using Base64-encoding and RTTY-100.

What I did is not new, by the way. Some of the first desktops and early
microcomputers
[used cassettes for data storage](http://en.wikipedia.org/wiki/Compact_Cassette#Data_recording).
The difference, however, is that they did not use RTTY (which was designed for
over-the-air text communications), and instead used
[FSK](http://en.wikipedia.org/wiki/Frequency-shift_keying)
(Frequency-shift Keying). As noted on Wikipedia, they could transfer data as a
rate up to 2000 bits/s, which results in a 660Kb capacity for a 90-minute tape.

n 2011, storing data on audio cassettes is pointless and impractical. However,
if you happen to have a tape and a tape recorder, it’s pretty fun to do it
anyway.

