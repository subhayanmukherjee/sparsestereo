# Fast stereo depth map from sparse depth estimates

My algorithm adopts a fast, hybrid approach (mixture of block and region based) for stereo disparity estimation from a rectified stereo image pair. It achieves error rates as low as 7.8%, 5.3% and 4.7% for three standard benchmark images (Tsukuba, Sawtooth and Venus) from the Middlebury stereo vision data-set, of sizes 384x288, 434x380 and 434x383 pixels respectively. The algorithm processes the above three image pairs within (an average of) 3 seconds on a PC having a Intel i7-2600 CPU @3.40 GHz and 8 GB RAM running Matlab 2013b on Windows 7. 

In a nutshell, I first convert the stereo image pair from R,G,B to L,a,b color space. Next, I perform intensity(L)-based segmentation of only left image pixels using a fast histogram-based K-Means implementation, then refine the segment boundaries using morphological filtering and connected components analysis. Then I determine the disparities of pixels constituting the refined boundaries using a block-based SAD approach, and lastly, fill in the (missing) disparities of pixels lying inside the refined segment boundaries (based on the refined boundaries' disparities already determined) using my simple and fast reconstruction method.



S. Mukherjee and R. M. R. Guddeti, "A hybrid algorithm for disparity calculation from sparse disparity estimates based on stereo vision," 2014 International Conference on Signal Processing and Communications (SPCOM), Bangalore, 2014, pp. 1-6.
doi: 10.1109/SPCOM.2014.6983949
