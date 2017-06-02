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

### Pipleline

My pipeline consists of five steps. First, I converted the images to grayscale, then I applied Gaussian blurring to the grayscale image. I used 5 for kernel size for this process that will remove salt-and-pepper noise. The next step was to detect edges from the blurred image using Canny. For this Canny, I used 5 and 150 for low and high threshold respectively. Then I detected straight lines using Hough transform in only a region of interest in which lane lines would exist.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by  followings. First, I separated all the lines into two groups (left and right) based on their slopes. All iines having positive slopes will be the right group. And the rest of the lines will be the left group. The slopes should be considered as opposite values with regard to those of the Cartesian coordinate system.  The small margin for the slope to zero was given because I did not want to have horizontal lines as lane lines. Also, I removed lines crossed the horizontal center of the image. Then I found the maximum and minimum values for x and y coordinates in each side separately. To draw one single line in the rigt side, I used two points: (minx, miny) and (maxx, maxy). To draw a single line in the left side, I used (minx, maxy) and (maxx, miny).

### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be liines would not be along with the actual lane lines because I did not collect potential points and averaged them.

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to collect clusters that are potential minimum and maximum values of x and y. Each clusters can get averaged to find more stable minimum and maximum x and y values.