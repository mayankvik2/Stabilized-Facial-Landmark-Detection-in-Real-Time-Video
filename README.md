# Stabilized-Facial-Landmark-Detection-in-Real-Time-Video
Kindly view attached research paper first for fully understanding probelm statements and concepts.

[Project Demo](https://www.linkedin.com/feed/update/urn:li:activity:6467719103737102336/)

One of the major challenges in Facial Landmark Detection on a real time video that it will not perform good under bad and inconsistent lighting conditions and starts jiggling landmark points. The most important reason for this instability is that the landmarks are detected in every frame independently and information in one frame is not tied with information of next frame. 

In this post I wrote a Python script for stabilizing facial landmark points in videos using below four different pieces of information and Optical Flow Estimation of Lucas Kanade. 

1. The location of a landmark in the current frame.
2. The location of the same landmark in the previous frame(s).
3. Pixels intensities in a small window in the current frame around the location of the landmark.
4. Pixels intensities in a small window in the previous frame around the location of the landmark in the previous frame.

## Optical Flow Estimation
Estimating the motion of every pixel in a sequence of images is a problem with many applications in computer vision such object classification,driver assistance etc and optical flow estimation can be used to develop algorithms to solve these challenges.

What is Optical Flow?

The optical flow at a point is simply the velocity vector of the point. It is given by
                      (u,v)=(dx/dt,dy/dt)
We want to calculate the optical flow at landmark locations, because once we have calculated the motion vector (u,v), we are able to predict the location of landmark in the next frame based on the current frame by simply adding the the motion vector to the landmark location.

### Algorithms implemented : Lucas-Kanade Optical Flow 
The algorithm is used for finding optical flow at discrete points.It makes assumption that in a small window centered at the feature point, the optical flow is the same for all pixels.

How Lucas- Kanade Optocal Flow handle large motion ?

Algorithms handles large motions using Image pyramids or Gaussian pyramids.The Gaussian Pyramid is produced by blurring the image using a Gaussian Kernel followed by downsizing the image by a factor of 2.
![alt text](https://github.com/mayankvik2/Stabilized-Facial-Landmark-Detection-in-Real-Time-Video/blob/master/ImagePyramid.png)

Using Image pyramids a more accurate optical flow is then recalculated for this new level using the optical flow from the previous level as an initial guess.
