The Writeup
---
The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw\_lines() function.

My pipeline consisted of 6 steps. First, I converted the images to `grayscale`, then I apply `Gaussian` smoothing the image, in order to reduce noise, actually, `Canny` applies Gaussian smoothing internally, but we include it here because you can get a different result by applying further smoothing. Canny function will find image edges, then we should  select interest region by  `mask`  image, next we connect the point  in the masked image use `HoughLinesP `,last merge origin image and 

In order to draw a single line on the left and right lanes, I modified the draw\_lines() function by thickness = 10.

If you'd like to include images to show how the pipeline works, here is show how the image change step by step:

*Gray:*

<img src="write_img/grayed.jpeg" width="480" alt="Combined Image" />

*Gaussian*

<img src="write_img/gaussian.jpeg" width="480" alt="Combined Image" />

*Edged（Canny）*

<img src="write_img/edged.jpeg" width="480" alt="Combined Image" />

*Mask*

<img src="write_img/masked.jpeg" width="480" alt="Combined Image" />

*Hough*

<img src="write_img/lined.jpeg" width="480" alt="Combined Image" />

*Merge*

<img src="write_img/weighted.jpeg" width="480" alt="Combined Image" />


---

### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be what would happen when Lane Lines is curved or the lane lines‘ gap is big, the pipeline is not accuracy. 

### 3. Suggest possible improvements to your pipeline
According to the algorithms I learned  now, I have no idea how to big improve the pipeline, or maybe I have not understand these algorithms totally.  


### Why we need hough space and how hough space find lines?

Hough space can map image line to a point and vise verse.
y = mx + b  line  in image space, map to (m, b) in hough space.
how to use is it to find line? 


when we convert a normal image to a edged image, if we zoom out it , we will see that the image consist by many points, our purpose is link these points to a line, we try different slope of lines to connect some points of all, and if the points number and points distance meet thresholds that we define , point (m, b) will be mapped into hough space.

Through many iteration of the operation above ,there have some points in the hough space, now we use these (m, b) points the draw the lines in the image.


<img src="write_img/houghlinesdemo.gif" width="480" alt="Combined Image" />


*here is question, how to get line length?*

blow is the definition of hough function:

	''rho = 2 # distance resolution in pixels of the Hough grid
	''theta = np.pi/180 # angular resolution in radians of the Hough grid
	''threshold = 35     # minimum number of votes (intersections in Hough grid cell)
	''min_line_len = 5  #minimum number of pixels making up a line
	''max_line_gap = 2    # maximum gap in pixels between connectable line segments
	''line_image = cv2.HoughLinesP(masked_edges, rho, theta, threshold, min_line_len, max_line_gap)

