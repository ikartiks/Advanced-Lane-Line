

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

**Camera Calibration**

The code for this step is contained in the 3rd 4th and 5th code cell of the IPython notebook located in "P1.ipynb"   

I start by preparing "object points", which will be the (x, y, z) coordinates of the chessboard corners in the world. Here I am assuming the chessboard is fixed on the (x, y) plane at z=0, such that the object points are the same for each calibration image.  Thus, `objp` is just a replicated array of coordinates, and `objpoints` will be appended with a copy of it every time I successfully detect all chessboard corners in a test image.  `imgpoints` will be appended with the (x, y) pixel position of each of the corners in the image plane with each successful chessboard detection.  

I then used the output `objpoints` and `imgpoints` to compute the camera calibration and distortion coefficients using the `cv2.calibrateCamera()` function.  I applied this distortion correction to the test image using the `cv2.undistort()` function and obtained this result: 

![distorrted image][writeup1.png]
![undistorrted image][writeup2.png]




**Example of a distortion-corrected image.**
To demonstrate this step, I will describe how I apply the distortion correction to one of the test images like this one:

![distorrted test image][writeup3.png]
![undistorrted test image][writeup4.png]

**Color and gradient Transforms**
The code for this is in the 2nd cell pipeline function. I used a combination of color and gradient thresholds to generate a binary image .  Here's an example of my output for this step.  (note: this is not actually from one of the test images)

![color and gradient transform][writeup5.png]

**Perspective Transform**

The code for my perspective transform includes a function called `warper()`, which appears 2nd code cell with function defined as warper. The `warper()` function takes as inputs an image (`img`), as well as source (`src`) and destination (`dst`) points.  I chose the hardcode the source and destination points in the following manner:

```
src=np.array([[240, 700], [580,460],[710,460], [1110,700] ],np.float32)
dst=np.array([[220, 700], [220,20],[1110 ,20], [1110,700] ],np.float32)

```

I verified that my perspective transform was working as expected by drawing the `src` and `dst` points onto a test image and its warped counterpart to verify that the lines appear parallel in the warped image.

![original image][writeup6.png]
![warped image][writeup7.png]

**I identify lane line pixles in 10th cell **

Then I did some other stuff and fit my lane lines with a 2nd order polynomial kinda like this:

![original image][writeup6.png]
![warped image][writeup7.png]

**I calculated the radius of curvature of the lane and the position of the vehicle with respect to center**

I did this in 2nd cell process_image function

**6. an example image lane line plotted in warped image.**

I implemented this step in lines # through # in my code in cell 12 and below is the resuly

![lane lines plotted][writeup10.png]

---

###Pipeline (video)

**Video link**.

Here's a [link to my video result](final.mp4)

---

###Discussion

####1. Problems and robustness

I will face a problem when my camera changes , i will have to recalibarate the camera and define src and dst points for transoformation. There should be an easier way to complete my perspective transform

