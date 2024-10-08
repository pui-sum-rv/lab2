# Plotting, Noise and Noise Removal

## Introduction to Matplotlib

Matplotlib is probably the most commonly used Python package for 2D graphics visualization. This package provides a fast way to visualize data from Python, as well as the ability to create high-quality images in many different formats.

`matplotlib.pyplot` is a collection of functions that make matplotlib behave similarly to MATLAB, making it easy for those with experience in MATLAB plotting to quickly adapt.

`matplotlib.pyplot` is _stateful_, which means it keeps track of the current figure, and all commands are directed at that figure.

### Simple Plots

In this section, we will show how to use matplotlib to plot some simple graphs. We'll start with the default settings, and then gradually improve the appearance of the graphs.
More information is provided in corresponding Jupyter notebook. 

## Noise

Wikipedia: [Image noise]( https://en.wikipedia.org/wiki/Image_noise )

### Gaussian noise

Gaussian noise represents statistical noise where the probability of a particular value occurring follows a normal or Gaussian distribution.

The probability of occurrence for a random value $z$ is given by:

![gauss formula](https://upload.wikimedia.org/math/c/7/0/c70012e2b38059f77ba8b6bb4cea7e2c.png)

where $z$ is the gray level, $\mu$ is the mean value, and $\sigma$ is the standard deviation.

The Gaussian distribution with given parameters $\mu$ and $\sigma$ looks like:

![gauss distrib](https://upload.wikimedia.org/wikipedia/commons/thumb/7/74/Normal_Distribution_PDF.svg/720px-Normal_Distribution_PDF.svg.png)

More about Gaussian noise: 

- [Gaussian distribution](https://en.wikipedia.org/wiki/Gaussian_distribution)
- [Gaussian noise](https://en.wikipedia.org/wiki/Gaussian_noise)

### Uniform noise


Uniform noise, also known as quantization noise, typically occurs during the quantization of pixel values in an input image to a certain number of discrete levels. It has an approximately uniform distribution, meaning that every value within a certain range has an equal probability of occurring.

![uniform_formula](https://upload.wikimedia.org/math/8/f/b/8fbfebfbb3dfa135da807a45374376d5.png)

where $a$ and $b$ are the boundaries within which a value can occur.

Here is what a uniform distribution looks like:

![uniform_dist](https://upload.wikimedia.org/wikipedia/commons/9/96/Uniform_Distribution_PDF_SVG.svg)

More about this topic can be found here:

- [ Quantization (Uniform) noise ](https://en.wikipedia.org/wiki/Image_noise#Quantization_noise_.28uniform_noise.29) 
- [ Uniform distribution ]( https://en.wikipedia.org/wiki/Uniform_distribution_%28continuous%29)

### Salt and pepper noise

Salt and pepper noise is a type of noise where a certain percentage of random pixels in the image are either white or black.

![snp](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f4/Noise_salt_and_pepper.png/220px-Noise_salt_and_pepper.png)

## Task 1

Load an arbitrary image and add Gaussian noise to it using the function defined above. Display the original image and the image with added noise in the same code cell. When displaying the images, set the `imshow` argument `cmap='gray'`. Assign a title to each image that corresponds to it (With Noise / Without Noise).

Tip: You can use `plt.show()` to display the current state on the screen and allow plotting of a new graph.

## Task 2

Using the `plt.hist` function, display the histogram of the original image and the image with added noise in the same code cell. Assign a title to each histogram. Set the `bins` parameter to the maximum value suitable for the image. Tip: Numpy arrays have a `.flatten()` method that converts the matrix into a 1D array of numbers.

## Task 3

Based on the `gaussian_noise` function and the formula for uniform noise above, implement a function that returns uniform noise for the parameters `a` and `b`.

Display in the same code cell the original image, the same image with Gaussian noise, and the same image with uniform noise.

# Median filtering

### Brief Description

The median filter is normally used to reduce noise
in an image, somewhat like the mean  (averaging) filter. However, it often does a
better job than the mean filter of preserving useful detail in the
image.


### How It Works

Like the mean (averaging) filter, the median filter considers each pixel in the
image in turn and looks at its nearby neighbors to decide whether or
not it is representative of its surroundings. Instead of simply
replacing the pixel value with the <EM>mean</EM> of neighboring pixel
values, it replaces it with the <EM>median</EM> of those values. The
median is calculated by first sorting all the pixel values from the
surrounding neighborhood into numerical order and then replacing the
pixel being considered with the middle pixel value.  (If the
neighborhood under consideration contains an even number of pixels,
the average of the two middle pixel values is used.) Following image 
illustrates an example calculation.

<CENTER><IMG ALT="" SRC="http://homepages.inf.ed.ac.uk/rbf/HIPR2/figs/med3x3.gif"></CENTER>

 Calculating the median value of a pixel neighborhood. As
can be seen, the central pixel value of 150 is rather unrepresentative
of the surrounding pixels and is replaced with the median value:
124. A 3&#215;3 square neighborhood is used here --- larger
neighborhoods will produce more severe smoothing.

### Guidelines for Use

<P>By calculating the median value of a neighborhood rather than the
mean value, the median filter has two main advantages over
the mean filter:

- The median is a more robust average than the mean and so a
single very unrepresentative pixel in a neighborhood will not affect
the median value significantly.

- Since the median value must actually be the value of one of the
pixels in the neighborhood, the median filter does not create new
unrealistic pixel values when the filter straddles an edge. For this
reason the median filter is much better at preserving sharp edges than
the mean filter.

You can use median filter with the following code:

```
median = cv2.medianBlur( image, radius )
```

where image is numpy array containing the image, and radius is an integer which
defines the radius of the neighborhood for filtering.

You can use gaussian blur filter with the following code:

```
blur = cv2.GaussianBlur( image, (kernelXsize, kernelYsize), sigma )
```

where image is numpy array containing the image, (kernelXsize, kernelYsize) is
a tuple containing the size of the kernel ( e.g. `(5, 5)` for 5x5 kernel ) and
sigma is the value of $`  \sigma  `$ parameter.

## Task 4

Corrupt an arbitrary image with 10% salt and pepper noise. Apply a median filter to the image and display the original and filtered images. Visually determine the best filter parameters that will remove the noise but not blur the image too much.
Apply Gaussian blur to the corrupted image and display the original and filtered images. Visually determine the best filter parameters that will remove the noise without blurring the image too much.

## Task 5

Corrupt an arbitrary image with Gaussian noise with sigma = 15. Apply a median filter to the image and display the original and filtered images. Visually determine the best filter parameters that will remove the noise without blurring the image too much.
Apply Gaussian blur to the corrupted image and display the original and filtered images. Visually determine the best filter parameters that will remove the noise without blurring the image too much.
