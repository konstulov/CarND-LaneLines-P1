# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/debug_example.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 7 steps.
In step 1 I performed color detection in the HSV space by filtering for yellow and white colors to detect yellow and white lines on the road.
In step 2, I grayscale the image and turn the white/yellow lines into pure white color (255) and every other pixel into black color (0).
Then I apply Gaussian Blur (step 3) with kernel size of 5, followed by Canny Edge Detector (step 4) and region of interest segmenter (step 5).
The cropped (RoI) output of Canny Edge detection is fed into a Hough Transform (step 6), which is then passed through a custom function combine_lines() (step 7) that combines the lines produced by Hough Transform by grouping the lines with the similar slopes and filtering out obvious noise using heuristics. The grouped lines are also extended to fit the expected length of a lane.

In order to help with the debugging process I wrote a function called process_img(img), which takes a NumPy array of an RGB image and plots the output of each step.

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming of the current pipeline is that it doesn't look very smooth on the videos due to the fact that slight variantions from frame to frame cause discrete changes in the detected lines.


### 3. Suggest possible improvements to your pipeline

A possible improvement to the pipeline could be to try and smooth out the line detections on consecutive frames in the video. This could possibly be achieved by simply averaging out the line positions of the current frame with the nearby frames.
