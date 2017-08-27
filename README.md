## Advanced Lane Finding
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

My submission of Udacity Self Driving Car Term1, Project 4. This project follows further from [Project 1](https://github.com/knguyen0105/CarND-LaneLines-P1). It employs advanced computer vision techniques to generalize a lane detection pipeline. Previous effort only detects lanes that are straight lines. In the project, we are able to detect curved lines. 

Sample video output:

![Sample Video Output](project_video_output.gif)

The Project
---

The goals / steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

Submission
---

- [IPython notebook](advanced-lane-finding.ipynb)
- [Project writeup](writeup.md)
- [Output video](project_video_output.mp4)

You might need to follow instructions on [CarND Term1 Starter Kit](https://github.com/udacity/CarND-Term1-Starter-Kit/) before running the notebook.
