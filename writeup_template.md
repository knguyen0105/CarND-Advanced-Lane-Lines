## Advanced Lane Finding Report

### Prepared by Khanh Nguyen (nguyen.h.khanh@gmail.com)

---

**Advanced Lane Finding Project**

The goals / steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

[//]: # (Image References)

[image1]: ./examples/undistort_output.png "Undistorted"
[image2a]: ./test_images/test1.jpg "Original Test Image"
[image2b]: ./examples/undistort__test1_output.png "Undistort Test Image"
[image3]: ./examples/binary_combo_example.jpg "Binary Example"
[image4]: ./examples/warped_test1.jpg "Warp Example"
[image5a]: ./examples/color_fit_lines.jpg "Fit Visual"
[image5b]: ./examples/color_fit_lines_band.jpg "Fit Visual Band"
[image6]: ./examples/test1_output.jpg "Output"
[video1]: ./project_video.mp4 "Video"

## [Rubric](https://review.udacity.com/#!/rubrics/571/view) Points

### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---

### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  [Here](https://github.com/udacity/CarND-Advanced-Lane-Lines/blob/master/writeup_template.md) is a template writeup for this project you can use as a guide and a starting point.  

You're reading it!

### Camera Calibration

#### 1. Briefly state how you computed the camera matrix and distortion coefficients. Provide an example of a distortion corrected calibration image.

*Note: All the code refered here are located after "Submission" section.

The code for this step is contained the function `collect_caliberation_points`. Here we assume a 9x6 chessboard. The function iterates through all calibration files in `camera_cal` folder and calculate data points for calibration. These points are stored at `objpoints` and `imgpoints`.

I then used the output `objpoints` and `imgpoints` to compute the camera calibration and distortion coefficients using the `cv2.calibrateCamera()` function.  I applied this distortion correction to the test image using the `cv2.undistort()` function and obtained this result: 

![alt text][image1]

### Pipeline (single images)

#### 1. Provide an example of a distortion-corrected image.

To demonstrate this step, I will describe how I apply the distortion correction to one of the test images like this one:
![alt text][image2a]

The result after applying distortion correction 

![alt text][image2b]

#### 2. Describe how (and identify where in your code) you used color transforms, gradients or other methods to create a thresholded binary image.  Provide an example of a binary image result.

I used a combination of color and gradient thresholds to generate a binary image. The code is contained in function `threshold`.  Here's an example of my output for this step to image in the previous step.

![alt text][image3]

#### 3. Describe how (and identify where in your code) you performed a perspective transform and provide an example of a transformed image.

Two sections of the code are involved in this task. The first part sets up four points to calculate the transformation.


```python
src_points_x = [200, 583, 703, 1100]
src_points_y = [img.shape[0], 460, 460, img.shape[0]]
dst_points_x = [300, 300, 1000, 1000]
dst_points_y = [img.shape[0],0, 0, img.shape[0]]
src = np.float32(list(zip(src_points_x, src_points_y)))
dst = np.float32(list(zip(dst_points_x, dst_points_y)))
M = cv2.getPerspectiveTransform(src, dst)
```

This resulted in the following source and destination points:

| Source        | Destination   | 
|:-------------:|:-------------:| 
| 200, 720      | 300, 720        | 
| 583, 460      | 300, 0      |
| 703, 460      | 1000, 0      |
| 1100, 720     | 1000, 720        |

I verified that my perspective transform was working as expected by drawing the `src` and `dst` points onto a test image and its warped counterpart to verify that the lines appear parallel in the warped image.

![alt text][image4]

#### 4. Describe how (and identify where in your code) you identified lane-line pixels and fit their positions with a polynomial?

I followed the sliding window approach described in the project resource. The result looks great.

![alt text][image5a]
![alt text][image5b]

#### 5. Describe how (and identify where in your code) you calculated the radius of curvature of the lane and the position of the vehicle with respect to center.

I did this in lines # through # in my code in `my_other_file.py`

#### 6. Provide an example image of your result plotted back down onto the road such that the lane area is identified clearly.

I implemented this step in lines # through # in my code in `yet_another_file.py` in the function `map_lane()`.  Here is an example of my result on a test image:

![alt text][image6]

---

### Pipeline (video)

#### 1. Provide a link to your final video output.  Your pipeline should perform reasonably well on the entire project video (wobbly lines are ok but no catastrophic failures that would cause the car to drive off the road!).

Here's a [link to my video result](./project_video_output.mp4)

---

### Discussion

#### 1. Briefly discuss any problems / issues you faced in your implementation of this project.  Where will your pipeline likely fail?  What could you do to make it more robust?

Here I'll talk about the approach I took, what techniques I used, what worked and why, where the pipeline might fail and how I might improve it if I were going to pursue this project further.  
