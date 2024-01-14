---
layout: post
title: "Lane Detection & Recognition"
subtitle: A Journey Through Computer Vision and Irish Roads
---

## Introduction to Lane Detection

In the rapidly evolving world of automotive safety, lane detection is a cornerstone technology. 
It's particularly crucial for the safe navigation of vehicles on diverse road conditions, 
such as the left-hand-drive, blustery conditions of the West of Ireland. 
In this project I explored a classical computer vision technique for lane detection & recognition on Sligo roads.

## Methodology Unpacked

The project, developed in Python3 and employing OpenCV, is hosted on my [GitHub](https://github.com/SenanS/Machine-Vision-Lane-Detection). 
It takes a unique (and perhaps not very good) approach to processing video stream data frame-by-frame, 
identifying lane markings, and overlaying them onto the original video feed.
![Detected Lane]({{ site.baseurl }}/public/LaneDet/DetectedLane.png){:class="img-responsive"}

### The Pre-processing Saga

Every frame undergoes a rigorous pre-processing routine:

1. **Area of Interest (AOI):** Frames are first masked to reduce computation to the essential, road-only view. 
This is achieved by defining a trapezoidal AOI based on preset coefficients.
2. **Grayscale Conversion and Edge Detection:** The image is converted to grayscale, blending the Blue-Green-Red (BGR) 
channels. The Sobel–Feldman operator is then applied to highlight edges.
3. **HSL Conversion and Thresholding:** Simultaneously, the BGR image is converted to a Hue-Luminance-Saturation (HSL) representation. 
The luminance is thresholded to accentuate the white or yellow lane markings, rather than tyre marks or fallen branches.
4. **Combination:** The HLS image is converted to greyscale and both images are logically ANDed together. Best of both.
5. **Blurring, Dilating and Eroding:** The combined image is blurred, converted to a binary image and a series of erosion and dilation operations are performed.
These morphological operations are effective in removing artefacts and noise remaining in the image, "opening" it.
6. **Canny Edge Detector:** Finally, the image is ready for the Canny edge detector, this will help to find lines in the image & is the last step before lane detection.

![Pre-Processing Flow]({{ site.baseurl }}/public/LaneDet/preproc.png){:class="img-responsive"}

### Lane Detection Mechanics
Post pre-processing, the Hough Transform algorithm comes into play..
* It identifies continuous lines in the image, discerning potential lane markings based on their slopes and continuity.
* Hough lines were discarded as probable lane markings using a trapezoidal bounded filtering method.
* Finally the lane lines were chosen based on the slopes and position in relation to the vehicle.

![Detection]({{ site.baseurl }}/public/LaneDet/detection.png){:class="img-responsive"}

## Concluding Thoughts and Beyond

This project is an example of traditional computer vision techniques in action. 
The future seems to incline towards AI and deep learning models for their adaptability and dynamism, especially 
under complex road conditions.
Though, it's still relevant and helpful to understand and implement classical methods of computer vision.

There are a plethora of methods to improve this algorithm, the obvious ones to me are to:
* Dynamic AOI - create an area of interest based only on the road in front. 
This would help when changing lanes, pulling onto a road & allow for data from different angles/ vehicles.
* Memory based lane markings - The estimation of lane markings based on expected road rules & immediately previous frame experiences. 
This could be particularly useful for the many Irish roads with faded & occluded boundaries.


Other ongoing research and projects are pushing the envelope in lane detection accuracy and robustness [^1].
It's clear that the path to safe automotive transportation is both challenging and exciting, with each 
new development paving the way for safer and smarter roads worldwide.

[^1]: N. J. Zakaria, Et al., "Lane Detection in Autonomous Vehicles: A Systematic Review," in IEEE Access, vol. 11, pp. 3729-3765, 2023, doi: [10.1109/ACCESS.2023.3234442](https://ieeexplore.ieee.org/abstract/document/10006813).
