---
layout: post
title: "Exploring Sensor Fusion in Vehicle Localisation and Tracking"
subtitle: 
---

<p>
Within this blog we'll explore an application of sensor fusion in vehicle localisation and tracking. 
It'll walk through the key concepts, methods, and reasoning behind the project. 
The blog aims to provide a clear understanding of how sensor fusion works in the niche context of tracking vehicles.</p>
<h3>
Getting Started: Understanding the Basics</h3>
<h4>
What is Sensor Fusion?</h4>
<p>
Sensor fusion involves combining data from multiple sensors to improve the accuracy of information. 
Using multiple sensors compensates for the limitations of individual sensors, offering a more reliable and accurate tracking system.
In vehicle tracking, this means using various external/internal sensors to precisely determine a vehicle's 
position and movement.</p>

<h4>What is The Project</h4>
<p>In this project, an eight-node sensor network will be used for vehicle tracking. 
This project provides a practical example of how sensor fusion can be implemented effectively.</p>

<h3>Step 1: Data Collection and Calibration</h3>
<h4>Calibration Mode</h4>
<ol>
	<li><strong>Setup</strong>: Position microphones equidistant from a stationary vehicle. 
	Assume the first microphone has a zero bias, all other mics are set relatively based on mic zero.</li>
	<li><strong>Purpose</strong>: To understand each microphone's bias, which is crucial for accurate data interpretation.</li>
</ol>
![Build-deploy]({{ site.baseurl }}/public/SenFu-Tracking/calibration.png){:class="img-responsive"}
<h4>Measurement Phase</h4>
<ol>
	<li><strong>Setup</strong>: Randomly place the same microphones around a track.</li>
	<li><strong>Action</strong>: Collect data as the vehicle moves.</li>
</ol>
![Build-deploy]({{ site.baseurl }}/public/SenFu-Tracking/vehicle-track.gif){:class="img-responsive"}

<h3>Step 2: Building Sensor Models</h3>
A time difference of arrival (TDOA) sensor network configuration knows the time of arrival of a measurement, but not the broadcast time.
The TOA can be modelled as proportional to the distance (between target and sensor) plus a bias.
<h4>Two different 2D 8-Sensor TDOA Models will be used</h4>
<ol>
	<li><strong>With Bias State</strong>: Accounts for biases in the sensor network.</li>
	<li><strong>With Pairwise Differences</strong>: Focuses on time differences between sensor pairs and the vehicle.</li>
</ol>
Analyzing with <strong>Cramer-Rao Lower Bound (CRLB)</strong> can help us understand the differences between these TDOA models.
The CRLB is a statistical method to estimate the lower bound of an estimator's variance, 
it helps in understanding the performance and reliability of your tracking system.</li>

![Build-deploy]({{ site.baseurl }}/public/SenFu-Tracking/CRLB.png){:class="img-responsive"}


<h3>Step 3: Localisation and Tracking Techniques</h3>
<h4>Using Weighted Least Squares (WLS) for Localisation</h4>
WLS is a method to minimize the differences between observed and predicted values. 
Here it's used for snapshot localisation, offering a practical approach to track the vehicle’s path accurately.

![Build-deploy]({{ site.baseurl }}/public/SenFu-Tracking/WLS.png){:class="img-responsive"}

Above are the localisation results using WLS with both TDOA networks. 
As is evident, they are poor approximations of the track. 
The errors were caused by sensors skipping measurement publish intervals, only to later re-align themselves.<br/>
The fix this the data was properly aligned, the new WLS comparisons are far more faithful to the ground truth.

![Build-deploy]({{ site.baseurl }}/public/SenFu-Tracking/WLS2.png){:class="img-responsive"}
 

<h4>Implementing Extended Kalman Filter (EKF) for Localisation</h4>
The EKF combines real-time measurements with a predictive model to estimate the vehicle's position and velocity.
It's performed in two sections, the Predictive state and the And the Update stage: The Innovation covariance is calculated, the optimal Kalman gain is computed, the
Corrected estimation is updated & the Covariance is updated.


![Build-deploy]({{ site.baseurl }}/public/SenFu-Tracking/EKF.png){:class="img-responsive"}

The EKF tracking here obviously underperforms compared to both the track and the WLS estimates.

<h3>Key Insights and Tips</h3>
<ol>
	<li><strong>Snapshot Localisation</strong>: Often more effective in scenarios where you need to track a vehicle at specific intervals.</li>
	<li><strong>Data Quality Matters</strong>: The accuracy of tracking improves with high-quality, real-world data.</li>
	<li><strong>Model Selection</strong>: The choice of sensor network and algorithms should align with your specific tracking needs.</li>
</ol>

<h3>Conclusion</h3>
<p>
Sensor fusion in vehicle localisation and tracking is a powerful technique that combines multiple data sources 
for enhanced accuracy. 
While TDOA1 & TDOA2 networks obviously differed in their variances & accuracies, the compute time for each should be considered before a best estimator can be crowned.
Similarly, the WLS outperformed the EKF for this specific application, that far-from invalidates the use of the EKF.
The principles and methods outlined can be applied to a multitude of different scenarios and data.
</p>

----

This post was based on my [GitHub repo](https://github.com/SenanS/Sensor-Fusion_Vehicle-Localisation-and-Tracking) 