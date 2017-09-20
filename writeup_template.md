# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

First, is the pre-processing of the image.  The image is converted to a one channel (grayscale) and blurred to reduce visual noise and artifacts.  This is necessary for the next step, finding the edges/outline of the lane lines.  In this step, we take advantage of the contrasting brightness of the lanes and their surrounding areas.  Using Canny Edge Detection, we identify pixels following the strongest gradients as well as adjacent pixels above a minimum threshold. In the next step, we create a mask which removes pixels outside of the region bound by the two converging lanes in front of the car.  


In order to draw a single line on the left and right lanes, I modified the draw_lines() function by separating x and y coordinates and gradients of the small lines from each lane.  Positive gradients belong to the left lane; negative to the right lane.  Using mean gradients and intercepts, we extrapolate lines to the two pixels with the minimum and maximum y-values. X-values are found with the line equation and the resulting x,y values are plugged into the OpenCV cv2.line() function to draw a line segment of desired color and thickness.


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the lanes curve?  The gradients of the left & right lanes may not be exact opposites. 

Another shortcoming could be the hardcoded region of interest.  The car would need to be positioned perfectly in the lane to capture the desired region of interest.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to allow for a dynamic region of interest.

Another potential improvement could be to modify the gradient to allow for curved lanes
