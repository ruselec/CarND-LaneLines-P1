**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

## Reflection

###1.

My pipeline consisted of 5 steps.

### Step 1
First, I converted the images to grayscale.

[image1]: ./pipeline/grayscale.jpg "Grayscale"

### Step 2
Then, I applied yellow and white filter. For that I converted the image to HSV color scheme. I chose the upper and lower values for yellow and white colors with help of this site: http://colorizer.org/. Then I combined masks for these colors and applied full mask on the grayscale.

[image2]: ./pipeline/filter.jpg "After filtering"

### Step 3

I blured image with gaussian blur.

[image3]: ./pipeline/blur.jpg "Blur"

### Step 4

I applied canny edge detector for left and right lines. Then, I defined region of interest for left and right lines and applied these masks to the image. I received two images: one for left and another for right.

[image4]: ./pipeline/left_edges.jpg "Left edges"

[image5]: ./pipeline/right_edges.jpg "Right edges"

### Step 5

I applied hough transformation to both images.

[image6]: ./pipeline/left_line.jpg "Left line"

[image7]: ./pipeline/right_line.jpg "Right line"

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by checking slope. Slope should be more than 0.3 for right line and less than -0.3 for left line. Then, I used points to find function for line and extrapolate it. Finally, I combined 3 images by weighted_img function. I increased coefficient a of this function to 0.9 so lines stay visible on final image.

[image8]: ./pipeline/final.jpg "Final"


![alt text][image1]


###2. Identify potential shortcomings with your current pipeline

* The current algorithm will be likely fall on curve road or snow road. 
* May be bright sunshine will distort the video input with glares and reflections.

###3. Suggest possible improvements to your pipeline

* To make the algorithm more robust I think to use polynominal line more than first order. 
* Also it should eliminate snow or water spots on the road to recognize lane lines correct
