---
layout: post
title: "Tap-Tap-Tapestry: A Wall-Projected Interactive DrumKit"
subtitle: 
---
<div class="container" style="display: flex; flex-wrap: wrap; align-items: center;">
    <img src="{{ site.baseurl }}/public/DrumKit/Drumkit.png" align="left" class="align-left" alt="Drumkit circuit representation" width="65%">

    <p style="flex: 1; margin-left: 20px" class="align-right">
        Ever fancied a drum-kit that won't take up half your living room, while still annoying your neighbours?
        Well, here's a solution that might just hit the right note: an interactive, wall-projected drum-kit.
        A nifty virtual kit that's a mix of clever electronics, lots of copper tape and a sprinkle of whimsy.
    </p>
</div>


## How it Works: A Symphony of Hardware and Software

The magic behind this project is a combination of Arduino and Processing sketches. 
The Arduino, a master of sensing inputs, waits for a tap on the capacitive switches, via copper tape, on the wall. 
Once it gets the signal, it sends the info over to the Processing sketch via serial communication.
The Arduino code is particularly simple, just sampling the capacitive switches and sending their state to Processing.

![Coppered Wall](https://raw.githubusercontent.com/SenanS/Interactive-Drumkit/main/Media/Wall-Coppered.jpeg){:class="img-responsive"}

<aside style="width: 39.5%">
    <p>
    For those who haven't used <a href="https://processing.org">Processing</a> I would greatly recommend it.
    It's fantastic tool for coding visual data representations, games or interfaces.
    Above all It is an easy, beautiful language.
    </p>
</aside>

<p>
The Processing sketch is where the visual and auditory magic happens. 
It creates the projected image of the drum-kit on the wall and plays the corresponding drum sounds. 
And after some fiddling with wire the project is complete. 
The drums are waiting.
</p>

<iframe
    width="100%"
    height="400px"
    src="https://www.youtube.com/embed/8VHfrf0_ESo?si=aWePd3thH20UroEy"
    title="YouTube video player"
    frameborder="0"
    allow="accelerometer;
        autoplay;
        clipboard-write;
        encrypted-media;
        gyroscope;
        picture-in-picture;
        web-share"> 
    Apologies, your browser doesn't support this video :(
</iframe>


## In Conclusion: Simple, Silly, and Satisfying

The project isn't breaking new ground in technology or art, but maybe it's a delightful blend of both. 
It's a testament to how a simple idea, some basic coding, and a bit of hardware can lead to hours of amusement. 
Whether you're a seasoned drummer or just someone who likes hitting walls, this project hits the right notes.

