# **Finding Lane Lines on the Road** 

## Writeup


---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"
[image2]: ./examples/example_1.jpg "example_1"

---

### Reflection

### 1. Pipleline

My image processing pipeline is consist of 5 steps. 

**(1) Get gray scale image** 
**(2) Apply Canny algorithm to get edges** 
**(3) Filter pixels in the central polygon area** 

We only cares the pixels in "central" area.

**(3) Apply Hough transform to get all lines** 

Hough transform returns many line segments (including noises) even with fine-tuned parameters.

**(4) Filter line segments by slope and length** 

Ignore the line segments of which the slope is too flat or vertical; and also only keep the line segments are longer than some threshold (like 50 pixels). These rules can effectively remove noises from output of hough transfrom.

**(5) Merge similar lines** 

Merging similar lines by checking line's slope and intercept. After lines are merged, ideally only 2 lines (left and right lanes) are left.

Merge strategy is that if 2 lines are "similar", remove one of them from line set.

**(6) Extend lines** 

Extend both lines to upper and lower area bound.


Finally will get this.


![alt text][image2]


### 2. Identify potential shortcomings with your current pipeline

One shortcoming is that since final line is extended from one shorter line segment, the error could be amplified when after extended.

Another thing is that the vertices of central ploygon are fixed points, the coordinates should depend on image's dimension.


### 3. Suggest possible improvements to your pipeline

One thing could be done is that when drawing current lines, it can be averaged with last lines to get a smoothier result.

