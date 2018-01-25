# **Finding Lane Lines on the Road** 



**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I applied Gaussian smoothing on the gray image as a way to suppressing noise. The next important step was using Canny method to detect the edges and output an appropriate grayscale image with white color edges. Then I used a four sided polygon to select the interested lane region approximately for further process. The last important step was to find pieces of lines  among Canny edges using the Hough Transform method.

In order to draw a single line on the left and right lanes,  I modified the draw_lines() function by averaging the lines to the left and right group. Concretely, the first step is to split the lines into two groups according their slopes.  Apparently, the slopes of line greater than zero belong to the left lane line and otherwise belong to the right. To get pair of average points in each group, just simply average the four numbers（x1, y1, x2, y2) respectively on each group. For each pair of points, I used ``np.polyfit`` method to figure out the line (y=ax+b) coefficients. Finally, using the known line formula to calculate the endpoints of the left and right lanes.



### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would detect lanes with big bias when encounter zebra crossing or other horizontal line crossing the lane. This is because by averaging lines the horizontal lines may dominant the result, outputing horizontal like lane.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to not include the lines which slope are near zero.
