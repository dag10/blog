---
layout: post
title: An open-source device for displaying upcoming events
date: 2014-03-02
tags: [arduino, c++, computer science house, flask, python]
content-folder: /post-content/2014/03/02/opensource-event-display
excerpt: 'Web and desktop projects are fun, but hardware adds a whole new dimension to
  software projects. I wanted to work on something physical, and I found the
  perfect application: A device that shows upcoming events on my floor’s lounge.
  I live in the Computer Science House at RIT and we
  have several special rooms, such as the lounge. We also maintain a shared
  Google Calendar, which is what my device pulls events from.'
---

![Event LCD installed outside lounge.]({{page.content-folder}}/installed.jpg)
*My upcoming-event display installed outside my dorm’s lounge.*

Web and desktop projects are fun, but hardware adds a whole new dimension to
software projects. I wanted to work on something *physical*, and I found the
perfect application: A device that shows upcoming events on my floor’s lounge.
<!-- more -->
I live in the *[Computer Science House](http://csh.rit.edu)* at RIT and we
have several special rooms, such as the lounge. We also maintain a shared
Google Calendar, which is what my device pulls events from.

The Hardware
------

<div class="image-right">
  <a href="http://oshpark.com/shared_projects/OAnGy2k5">
    <img src="{{page.content-folder}}/pcb.png" />
  </a>
  <em>Render of custom PCB.</em>
</div>
It starts with an [Arduino Ethernet](http://www.amazon.com/gp/product/B005D22FR6/ref=oh_details_o03_s00_i00),
which is basically an Arduino Uno with the ethernet shield built-in. It also
comes with a POE (Power over Ethernet) module, which is something I didn’t
realize existed before this project. For the display, I’m using a 4×20
character [LCD](http://www.amazon.com/gp/product/B00D7Z2BWU/ref=oh_details_o09_s00_i01),
based on the popular HD44780 LCD controller. The controller’s popularity
means that there are many resources and libraries for interfacing with it,
especially from an Arduino. To conserve pins for future hardware additions,
such as buttons or RFID readers, I opted to use a [74LS595](http://www.ti.com/lit/ds/symlink/sn74ls595.pdf)
shift register to interface with the LCD. Because of the shift register,
the wiring, and the required 10k trim potentiometer needed for the contrast
adjustment, I decided to [create](http://oshpark.com/shared_projects/OAnGy2k5)
a printed circuit board to bridge the LCD module with the LCD.

Finally, I found an old, plastic “project enclosure” laying around. I have no
idea where it came from, but it was the perfect size for my electronics. After
some dremeling, it had holes for the LCD and the ethernet port.

![Inside of device]({{page.content-folder}}/inside.jpg)
*The assembled device without the back cover.*

Finally, up on the wall it goes. I ran cat5e cable in the ceiling from the
lounge to my floor’s networking room, and mounted a raceway on the wall to
hide the cable. In the networking room, I installed the power-over-ethernet
injector, and the device sprang to life.

The Software
------

There are two programs: The Arduino program written in C++, and a server-side
web server written in Python, using the [Flask](http://flask.pocoo.org/) web
framework. The server connects to the Google calendar and gets the next events
in a requested location. Then it outputs the text exactly as the LCD should
display it.

I was originally going to have the server return JSON data of the upcoming
events, and the Arduino would parse this data and format it for the screen.
This was before I realized that the ATmega328 has only 2K of RAM, which is
simply not enough for both an HTTP client and a JSON parser. This is why I
decided to offload the text formatting to the server itself. I later realized
an additional benefit this adds: I can tweak what the LCD displays without
having to update the firmware or touch the device in any way.

------

More details and instructions on how to build your own can be found in the
project’s readme on GitHub: More details and instructions on how to build your
own can be found in the project’s readme on GitHub:
<a href="https://github.com/dag10/EventLCD">https://github.com/dag10/EventLCD</a>

