# Linear Revolution-Invariance: Modeling and Deblurring Spatially-Varying Imaging Systems

[![Paper](https://img.shields.io/badge/paper-%09arXiv%3A2003.12673-yellow.svg)](https://arxiv.org/abs/2206.08928)

## Background
Official implementation of Linear Revolution-Invariant modeling and deblurring. 

LRI forward modeling allows one to compute the output of any rotationally symmetric imaging system given only a few of its PSFs or its Seidel aberration coefficients. Simiarly, LRI deblurring offers a fast and more accurate alternative to deconvolution (e.g., Wiener filter, Richardson-Lucy) by accounting for radially-varying blur. LRI deblurring only requires a single calibration image of a few randomly scattered PSFs.

This repository is still in early stages and will constantly be updated with new functionality. It is on its way to becoming a PyPI python package!

## Useage

For now, to run the LRI forward model and LRI deblurring please see follow along with ```test.py```. A Jupyter notebook will be added shortly. 

There are 3 main functions of interest located in ```functions.py```:

**1) calibrate**

Here we pass in either a calibration image such as ```test_images/calibration_image.tif``` or Seidel aberration coefficients (i.e., [sphere, astigmatism, coma, field curvature, distortion]). We get back a stack of the rotational fourier transforms (see paper appendix E) of PSFs along a radial line and the Seidel coefficients.
```
psf_stack_roft, seidel_coeffs = calibrate(calib_image, dimension, num_radii, seidel_coeffs)
```
**2a) blur**

With PSFs in hand we can simulate the blurring of an imaging system using the LRI forward model. We simply pass in a test object such as ```test_images/baboon.png``` and our PSF stack obtained from the calibration step.
```
blurred_image = blur(object, psf_stack_roft)
```

**2b) deblur**

Alternatively we can choose to invert the LRI forward model to instead perform image deblurring. Again we only need the PSF stack from step 1 in addition to the blurry image we would like to deblur.
```
deblurred_image = deblur(blurred_image, psf_stack_roft)
```

This is the basic procedure; more details can be found in ```test.py```.


The necessary packages to run this code are:
* numpy
* pytorch
* scipy
* skimage
* PIL
* cv2
* matplotlib
* tqdm


## Contact
Please reach out to apkohli@berkeley.edu with any questions or concerns!

