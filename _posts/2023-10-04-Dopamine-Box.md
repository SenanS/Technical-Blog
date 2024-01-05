---
layout: post
title: "The Dopamine Box"
subtitle: 
---

A flip switch circuit for encouraging you to complete tasks, loaded with lights and achievement sounds.

![The Dopamine Box](https://raw.githubusercontent.com/SenanS/Dopamine-Box/main/Images/Box%20Front.jpg)

This project was conceptualized and designed by me, to gamify mundane tasks. It tracks up to five tasks, offering audiovisual feedback upon completion of each task, effectively rewarding the user with a dopamine hit.

This project was more than just a tool for self-motivation; I used it as a springboard to dive into the realms of audio amplifiers and probability distributions.

## Delving into the Heart of the Dopamine Box
The heart of this project lies in its `Arduino` code, which can be found in the [Dopamine-Box.ino file](https://github.com/SenanS/Dopamine-Box/blob/main/Dopamine-Box.ino). 
This code is responsible for the operational logic of the box, from tracking the flip switches to triggering the lights and sounds upon task completion.

### Key Interactions for the Project:
1. **Task Tracking:** Utilizes digital I/O pins to monitor the state of each flip switch.
2. **Audio Feedback:** Leverages an audio module to play sounds when a task is completed.
3. **Visual Feedback:** Controls an array of LEDs to visually indicate task progress and completion.
4. **Haptic Feedback:** Who doesn't enjoy the satisfying *snap* of a throw switch.

### Task Tracking:
The task completion triggers logic was as simple as it comes, the switches were polled in the main loop, waiting for an increase in the state count (number of switches flipped).

### Audio Feedback:
By integrating an amplifier with the Arduino, the box produces a distinct sound each time a task is completed, amplifying the user's sense of achievement.

I chose sounds from a variety of sources, mostly game franchises like Mario, Sonic, Legend of Zelda, etc.
I broke the 23 sounds into 5 categories, based on the expected dopamine hit. 

<aside><p>
    For my brain, the <a href="https://www.youtube.com/watch?v=mQSmVZU5EL4">Mario coin noise</a> was a category 1 dopamine hit. 
    <audio controls>
        <source src="{{ site.baseurl }}/public/Dopamine/a2.wav" type="audio/mpeg">
        Your browser does not support the audio element.
    </audio>
    While the <a href="https://www.youtube.com/watch?v=5VRr9NG7RE0">Zelda chest noise</a> was a category 5.
    <audio controls>
        <source src="{{ site.baseurl }}/public/Dopamine/f0.wav" type="audio/mpeg">
        Your browser does not support the audio element.
    </audio>
</p></aside>

### Audio Amplification
The audio was pre-loaded onto an SD card (I fear to share it all for copyright infringement).
In my first foray into audio amplification I used an [LM386 Low Voltage Power Amp](https://www.ti.com/lit/ds/symlink/lm386.pdf) and a recycled speaker I'd harvested from an old device.
Tuning the circuit was definitely the most difficult part of this project.
Trying to achieve the highest signal gain while minimising the noise was an interesting process.

### Probability Distributions for Happiness Contributions
<aside><p>
    The five categories were :
    <ul>
        <li>Dopamine Level 1 (A)</li>
        <li>Dopamine Level 2 (B)</li>
        <li>Dopamine Level 3 (C)</li>
        <li>Special Sounds   (X)</li>
        <li>Finale Sounds    (F)</li>
    </ul>
</p></aside>

The most enjoyable part of this project was creating a state dependant probability distribution to play the 5 categories of feedback sound.

I believe the probability distribution helped to keep the task rewards unpredictable, and therefore keeping the Dopamine Box re-usable.

```C
{% raw %}
// Probability of output:       A,    B,    C,    X,    F},
int outputProbability[5][5] = {{80,   10,   7,    3,    0},
                               {30,   50,   15,   5,    0},
                               {5,    70,   22,   3,    0},
                               {0,    10,   85,   3,    2},
                               {0,    0,    0,    0,    100}
                              };
{% endraw %}
```
The columns of the above matrix represent the 5 categories of Dopamine level, while the rows represented the state count (cumulative number of switches flipped).

When a new switch is flipped, the corresponding state row is selected (eg. ```state = 2, outputArray = {5, 70, 22, 3, 0}```).
The category probabilities are treated like a number line, where a randomised value is generated between 1-100 & the audio category chosen is based on the location of the randomised point on the number line.  
![Audio Category]({{ site.baseurl }}/public/Dopamine/RandVal.png){:class="img-responsive"}

## Electronics
 Finally, all was left was to select components, breadboard prototyping & stripboard soldering.


[Board Schema](Schema.pdf) | [Stripboard Schema](Stripboard.pdf)
:-------------------------:|:-------------------------:
![Schema](https://user-images.githubusercontent.com/30498489/143792116-d8c3bf85-45dd-46d5-a239-992edfecd1a4.jpg){:class="img-responsive"} | ![Stripboard](https://github.com/SenanS/Dopamine-Box/assets/30498489/4344cf08-0fb6-437d-9f40-663cb631e6e3){:class="img-responsive"}

## Conclusions
The Dopamine Box project was an enriching journey, blending electronics, programming, and psychological elements to create a unique, one-of-a-kind box? tool? e-waste? 

At some point, I'd like to update it with a nicer chassis, perhaps an internet connection to pull hundreds of reward sounds & more enriching feedback! 
![DopBoxLit](https://raw.githubusercontent.com/SenanS/Dopamine-Box/main/Images/Box%20Lit.jpg){:class="img-responsive"}

---

All schematics, code & 3D model files can be found in the [Github repo](https://github.com/SenanS/Dopamine-Box/tree/main).