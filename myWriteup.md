#**Finding Lane Lines on the Road** 

##Boyin's Writeup

###Week 1

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)



---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale.
[grayscale]: ./test_images/solidWhiteCurve_gray.jpg "Grayscale"

Then I use Gaussian smoothing to suppress noise and spurious gradients. 

After that, I use Canny function to find the edge of the picture. 
[edges]: ./test_images/solidWhiteCurve_edges.jpg

In step 4, since some structures near or above the road, like streetlights and billboards, where many lines could be detected in next step, I add a mask which makes "road" is the only part of the image can be detected. 

Finally, I use Hough Transformation to identify and paint the lines that stands for the edges of road. 
[hough]: ./test_images/solidWhiteCurve_hough.jpg

And combine it with original image.
[result]: ./test_images/solidWhiteCurve_lines_edges.jpg
(I don't know why the colour in these two pictures are so weird here. They are good in the result of code)

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by changing the thickness. In 'white.mp4', there is always a supering line shows in the button of the video. So I increase the threshold of Canny function(i.e. enhance the threshold of "being a line"). It is not difficult to annotate solid line as a line because it has already been, but separate line is not. I have turned parameters of Hough Transformation function to ensure minimum number of votes is not too big, maximum gap in pixels bteween connecttable line segments is large enough.


###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be that line might be hard to detecte  when there is a big curve. Also the view region should be changed when turn the car. But the mask is fixed.

Another shortcoming could be light and shadows may cause confusion because they also bring edges.

Meanwhile, when another car cut in, with the refection of the lignt, there could be some unexpected lines annotated.



###3. Suggest possible improvements to your pipeline

A possible improvement would be to add a colour-select function to eleminate surprising lines on road.

Another potential improvement could be to dynamic define the mask. 