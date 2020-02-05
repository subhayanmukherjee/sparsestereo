# Fast stereo depth map from sparse depth estimates

My algorithm adopts a fast, hybrid approach (mixture of block and region based) for stereo disparity estimation from a rectified stereo image pair. It achieves error rates as low as 7.8%, 5.3% and 4.7% for three standard benchmark images (Tsukuba, Sawtooth and Venus) from the Middlebury stereo vision data-set, of sizes 384x288, 434x380 and 434x383 pixels respectively. The algorithm processes the above three image pairs within (an average of) 3 seconds on a PC having a Intel i7-2600 CPU @3.40 GHz and 8 GB RAM running Matlab 2013b on Windows 7. 

In a nutshell, I first convert the stereo image pair from R,G,B to L,a,b color space. Next, I perform intensity(L)-based segmentation of only left image pixels using a fast histogram-based K-Means implementation, then refine the segment boundaries using morphological filtering and connected components analysis. Then I determine the disparities of pixels constituting the refined boundaries using a block-based SAD approach, and lastly, fill in the (missing) disparities of pixels lying inside the refined segment boundaries (based on the refined boundaries' disparities already determined) using my simple and fast reconstruction method.

Please cite the below [paper](https://doi.org/10.1109/SPCOM.2014.6983949) if you use the code in its original or modified form:

*S. Mukherjee and R. M. R. Guddeti, "A hybrid algorithm for disparity calculation from sparse disparity estimates based on stereo vision," 2014 International Conference on Signal Processing and Communications (SPCOM), Bangalore, 2014, pp. 1-6.*

# Guidelines

1. Download all files to the same folder.

2. To run the algorithm on the provided rectified stereo image pair, execute the following MATLAB command and see the output:
	imshow(StereoDisp('im_left.png', 'im_right.png', 10, 15, 9, 16))

3. You can also open the provided ground truth disparity map for the left image 'truedisp_left.png' and compare it with my output.

4. Also included is a (down-scaled) stereo frame extracted from a 3D video recorded in our lab using our Sony HDR-TD10 3D camcorder
('cam_left.jpeg' and 'cam_right.jpeg') and the output (left image) depth map ('cam_depth_left.png') after running our algorithm:
	imshow(StereoDisp('cam_left.jpeg', 'cam_right.jpeg', 15, 25, 7, 10))

The image files and parameter values mentioned in points 2 and 3 have all been taken from the Middlebury stereo vision dataset [1]:
http://vision.middlebury.edu/stereo/data/

The FastCMeans.m and LUT2label.m files have been taken from Anton Semechko's "Fast segmentation of N-dimensional grayscale images":
http://www.mathworks.in/matlabcentral/fileexchange/41967-fast-segmentation-of-n-dimensional-grayscale-images/content/FastCMeans.m

## References

[1]	D. Scharstein and R. Szeliski. A taxonomy and evaluation of dense two-frame stereo correspondence algorithms.
International Journal of Computer Vision, 47(1/2/3):7-42, April-June 2002.
