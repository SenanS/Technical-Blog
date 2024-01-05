---
layout: post
title: "Tap-Tap-Tapestry: A Wall-Projected Interactive DrumKit"
subtitle: 
---

<iframe 
    width="560"
    height="315"
    src="https://www.youtube.com/embed/8VHfrf0_ESo?si=aWePd3thH20UroEy" 
    title="YouTube video player" 
    frameborder="0" 
    allow="accelerometer; 
        autoplay; 
        clipboard-write; 
        encrypted-media; 
        gyroscope; 
        picture-in-picture; 
        web-share"> Apologies, your browser doesn't support this video :(
</iframe>

<div style="clear: both;">
    <div style="float: left; margin-right 1em;">
        <img src="{{ site.baseurl }}/public/DrumKit/Drumkit.png" alt="Drumkit-header">
    </div>
    <div>
        <p>
            Ever fancied a drum-kit that won't take up half your living room, while still annoying your neighbours? 
            Well, here's a solution that might just hit the right note: an interactive, wall-projected drum-kit. 
            A nifty virtual kit that's a mix of clever electronics and a dash of whimsy.
        </p>
    </div>
</div>

## How it Works: A Symphony of Hardware and Software

The heart of this musical contraption is a set of capacitive switches mounted on a wall. 
These switches, more sensitive than a musician's ego, are controlled by an Arduino. 
Here's a snippet of the Arduino code that gets this party started:

arduino

#include <CapacitiveSensor.h>

// Cap sensor pins
CapacitiveSensor   cs_2_4 = CapacitiveSensor(2,4);        
CapacitiveSensor   cs_2_5 = CapacitiveSensor(2,5);        
CapacitiveSensor   cs_2_6 = CapacitiveSensor(2,6);        
// more sensor initializations here...

void setup()                    
{
Serial.begin(9600);
}

void loop()                    
{
long start = millis();
long total1 =  cs_2_4.capacitiveSensor(30);
long total2 =  cs_2_5.capacitiveSensor(30);
long total3 =  cs_2_6.capacitiveSensor(30);
// more sensor readings here...

    Serial.print(millis() - start);       
    Serial.print("\t");                   
    Serial.print(total1);                  
    Serial.print("\t");
    Serial.print(total2);                  
    Serial.print("\t");
    Serial.println(total3);                
    // more print statements...
}

Snippet from DrumCode.ino

Each tap on these switches is like striking a drum, sending a signal to the Arduino. The Arduino then chats with a Processing sketch over serial communication. This sketch is the visual maestro, creating an image of the drumkit and outputting the corresponding drum sounds. Check out this piece of the Processing sketch:

java

import processing.serial.*;

Serial myPort;  
String val;

void setup()
{
size(640, 360);
// I know, we're using size() outside of settings(). It's a rebel move.
println(Serial.list());
String portName = Serial.list()[0];
myPort = new Serial(this, portName, 9600);
}

void draw() {
if ( myPort.available() > 0) {  // If data is available,
val = myPort.readStringUntil('\n');         // read it and store it in val
}
if (val != null) {
background(0);               // Set background to black
if (val.equals("something")) {
// drum hit actions here
}
}
}

Snippet from drumkit.pde
Visuals and Sounds: The Setup

The setup is surprisingly simple. A projector beams the image of a drumkit onto a wall. Here's a look at the setup process, showing how this whimsical idea materializes into something you can actually play.

And voilà! Once you're done setting it up, you have a drumkit that's as visually striking as it is fun to play. Here's the final look:

In Conclusion: Simple, Silly, and Satisfying

This project isn't breaking new ground in technology or art, but it's a delightful blend of both. 
It's a testament to how a simple idea, some basic coding, and a bit of hardware can lead to hours of amusement. 
Whether you're a tinkerer, a music enthusiast, or just someone who likes hitting walls, this project hits all the right notes.
