## Advanced Lane Finding

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

---

### How To run

Please review the installation instructions [here](https://github.com/udacity/CarND-Advanced-Lane-Lines/blob/master/README.md)

---

![alt text][image2]

---

[//]: # (Image References)

[image1]: ./output_images/undistort_output.png "Undistorted"
[image2]: ./output_images/demo.gif "Demo"
[image3]: ./output_images/binary_combo_example.jpg "Binary Example"
[image4]: ./output_images/image4.JPG "diagrams"
[image5]: ./output_images/Calib.JPG "Calibration"
[image6]: ./output_images/example_output.jpg "Output"
[video1]: ./project_video.mp4 "Video"


### Camera Calibration

#### 1. Briefly state how you computed the camera matrix and distortion coefficients. Provide an example of a distortion corrected calibration image.

OpenCV functions `findChessboardCorners` and `drawChessboardCorners` help identify the locations of corners on a series of pictures of a chessboard taken from different angles. Here's the code I used for camera calibration:


![alt text][image5]

### Distortion Correction

It is important to correct for image distortion because distortion can change the apparent size or shape of an object in an image, it can also cause an object's appearance to change depending on where it is in the field of view. Distortion can make objects appear closer or farther away than they actually are.

To undistort an image, I used 20 images of chess boards that are taken from a different perspective. They are great for calibration thanks to their high contrast pattern makes it easy to detect automatically. `cv2.undistort()` function of `OpenCV` helps do the job!

![alt text][image1]

### Binary thresholds 

Binary threshold images help isolate only the pixels belonging to lane lines. To convert the warped image to different color spaces and create binary thresholded images, I used the absolute Sobel threshold, the magnitude Sobel threshold, and the directional Sobel threshold.

![alt text][image3]


**Perspective transform**

The objective here is to transform the undistorted image to a "birds eye" view that focuses only on the lane lines and displays them in such a way that they appear to be relatively parallel. This was a necesary step because it is much easier to determine lane curvature from this perspective.

**Fitting a polynomial** 

The next step is to fit a polynomial to each lane line, for that I:
- Identified peaks in a histogram of the image to determine location of lane lines.
- Identified all non zero pixels around histogram peaks using the numpy function `numpy.nonzero()`.
- Found a polynomial to each lane using the numpy function `numpy.polyfit()`.

![alt text][image4]

---

### Pipeline (video)

Here's a [link to my video result](./project_video_OUTPUT.mp4)

### Discussion

This pipeline can be challenged with changing weather conditions, road quality, lighting, and different types of driving conditions like lane shifts and exiting.
