# The Dopamine Box
A flip switch circuit for encouraging you to complete tasks, loaded with lights and achievement sounds.

![The Dopamine Box](https://raw.githubusercontent.com/SenanS/Dopamine-Box/main/Images/Box%20Front.jpg)

This project was conceptualized and designed by me, to gamify mundane tasks. It tracks up to five tasks, offering audiovisual feedback upon completion of each task, effectively rewarding the user with a dopamine hit.

This project was more than just a tool for self-motivation; I used it as a springboard to dive into the realms of audio amplifiers and probability distributions.

## Delving into the Heart of the Dopamine Box
The heart of this project lies in its `Arduino` code, which can be found in the [Dopamine-Box.ino file](https://github.com/SenanS/Dopamine-Box/blob/main/Dopamine-Box.ino). 
This code is responsible for the operational logic of the box, from tracking the flip switches to triggering the lights and sounds upon task completion.

### Key Features of the Code:
1. **Task Tracking:** Utilizes digital I/O pins to monitor the state of each flip switch.
2. **Audio Feedback:** Leverages an audio module to play sounds when a task is completed.
3. **Visual Feedback:** Controls an array of LEDs to visually indicate task progress and completion.

### Task Tracking:
The task completion triggers logic was as simple as it comes, the switches were polled in the main loop, waiting for an increase in the state count (number of switches flipped).

### Audio Feedback:
By integrating an amplifier with the Arduino, the box produces a distinct sound each time a task is completed, amplifying the user's sense of achievement.

I chose sounds from a variety of sources, mostly game franchises like Mario, Sonic, Legend of Zelda, etc.
I broke the 23 sounds into 5 categories, based on the expected dopamine hit (i.e. the [mario coin noise](https://www.youtube.com/watch?v=mQSmVZU5EL4) was a category 1, while the [Zelda chest noise](https://www.youtube.com/watch?v=5VRr9NG7RE0) was a category 5)

[//]: # ({% include embed-audio.html src='{{ site.baseurl }}/public/Dopamine/a2.wav' %})

 <audio controls>
    <source src="{{ site.baseurl }}/public/Dopamine/a2.wav" type="audio/mpeg">
    Your browser does not support the audio element.
</audio>

```arduino
// Check if a task is completed
if (digitalRead(taskSwitch) == HIGH) {
    // Play completion sound
    playSound(taskCompleteSound);
    // Illuminate corresponding LED
    digitalWrite(ledPin, HIGH);
}
```

## Electronics

[Board Schema](Schema.pdf) | [Stripboard Schema](Stripboard.pdf)
:-------------------------:|:-------------------------:
![Schema](https://user-images.githubusercontent.com/30498489/143792116-d8c3bf85-45dd-46d5-a239-992edfecd1a4.jpg) | ![Stripboard](https://github.com/SenanS/Dopamine-Box/assets/30498489/4344cf08-0fb6-437d-9f40-663cb631e6e3)
