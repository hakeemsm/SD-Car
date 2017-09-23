# **Finding Lane Lines on the Road** 
# **This work is submitted by Hakeem S Mohammad for Term1 in the Udacity Self Driving Car nano-degree**


The goals / steps of this project were:
* Building a pipeline to find lane lines on the road
* Description of the techniques in this report


[//]: # (Image References)

[whiteCarLaneSwitch]: ./test_images_output/whiteCarLaneSwitch "White car lane switch"
[solidYellowCurve]: ./test_images_output/solidYellowCurve2 "Solid yellow curve"
[solidWhiteRight]: ./test_images_output/solidWhiteRight "Solid white right"

---

### Reflection

### 1. The steps below describe the steps in the pipeline and also the changes that were done to the draw_lines() function

* Convert the image to gray scale
* Apply Guassian blur with a kernel size of 5
* Apply Canny to the image produced by Guassian blur with a low threshold of 50 and high threshold of 150
* Determine the vertices for the lanes and build an array large enough for the image with the apex points
* Calculate the region of interest for the image returned by canny using the vertices. The region_of_interest() function returns a masked image after applying fillPoly
* Apply the HoughLinesP() method to calculate the hough lines for the masked image. The provided hough_lines() function calls draw_lines() function to draw the lines using CV
* The draw_lines() function has been updated so that it first calculates the slope for each pair of coordinates and determines whether they belong to the left lane or right lane. It builds an array of x and y points for each side and uses the min, max and average values from those arrays to draw lines from the apex to the edges using cv2.
* Below are some of the images rendered with this pipeline


![alt text][whiteCarLaneSwitch]
![alt text][solidYellowCurve]
![alt text][solidWhiteRight]


### 2. Shortcomings

While the lanes and apex points hold well for all alignments, there are a few sharp variations on occasion for the X coordinates for both lanes. This is owing to the fact that the draw_lines() function takes min, max or average based on the slope values and in situations where there is a curve, the slope changes drastically from the previous value and therefore affects the x values chosen for the line edges


### 3. Possible improvments

The flicker observed for some data points due to angle changes can be eliminated by accurately calculating the horizontal axes and drawing lines using those coordinates