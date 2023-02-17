# Image-Compression-and-Denoising-by-SVD-and-FFT
### Singular Value Decomposition (SVD)
![Screenshot (63)](https://user-images.githubusercontent.com/125180530/219767700-b1bbeefc-6642-419e-b639-1593aba1d8e9.png)

![Screenshot (61)](https://user-images.githubusercontent.com/125180530/219766029-ca9ea513-5577-4717-bf86-b5fb9f201e36.png)

### Compression Using SVD
We often need to transmit and store the images in many applications. Smaller the image, less is the cost associated with transmission and storage. So we often need to apply data compression techniques to reduce the storage space consumed by the image. One approach is to apply Singular Value Decomposition (SVD) on the image matrix. In this method, digital image is given to SVD. SVD refactors the given digital image into three matrices. Singular values are used to refactor the image and at the end of this process, image is represented with smaller set of values, hence reducing the storage space required by the image. Goal here is to achieve the image compression while preserving the important features which describe the original image. SVD can be adapted to any arbitrary, square, reversible and non-reversible matrix of m × n size. Compression ratio and Mean Square Error is used as performance metrics.

### Fast Fourier Transform (FFT)
A Fourier transform allows deconstructs an image to its frequncy domain. In this domain, one can remove insignificant frequncies, essentially stripping data from the image. One can then reconstruct the image with less frequncies to obtain a "compressed" image. For the sake of simplicity, image width and height are constrained to be a power of two and all images are greyscaled before fourier transform computations.

### Compression Using FFT
After a fourier transform is done, the frequncies are sorted and only a certain fraction of frequncies are kept, the rest of the data in the matrix is set to 0. Finding exactly which data to keep is the often very slow with large data matrices. Such precision is usually not neccesary and a randoming sampling to approximated the distribution of the frequncies and then choosing a cut-off would have been much more faster than finding the exact cut-off. 

A quick and easy way to do image compression then, is to convert an image to frequency space, find the lowest amplitude frequencies and throw them away – literally zero out the complex number. If you throw enough of them away, it’ll take less data to describe the frequency content of an image, than the pixels of the image, and you’ll have compressed the image.

The more aggressive you are at throwing away frequencies though, the more the image quality will degrade. This is “lossy” compression and is a simplified version of how jpg image compression works. 

* First of all, we change the images to gray-scale. Then we write functions for SVD and FFT compression for the following compression ratios:

ratios = {0.1 , 0.5 , 1 , 4 , 8 , 10 , 12}

* We then compare the compressed images of the two methods.

### Comparison of SVD and FFT in Image Compression
SVD is the factorization of a real or complex matrix, while FFT is an algorithm which allows low pass and high pass filtering with a great degree of accuracy. FFT is also a process that vastly reduces the time needed to compute large matrices. Distortion and compression ratios for each method were calculated at different parameters. Images were compressed without sacrificing significant image quality. Comparing the compression ratio, distortion, and visual quality of the images, FFT was determined to be the better of the two compression methods.

* For RGB format, we implement both of the previous algorithms. In this case, we need to do the same process for each of the three RGB channels separately. 

### SVD Method for Image Denoising 
SVD denoising is similar to image compression. In this way, we obtain the SVD transformation of the image matrix and then according to the value we have determined for rank, we keep the same number of singular values and their corresponding eigenvectors and set the rest of the singular values and vectors to zero. In this situation, similar to the previous one, instead of setting the smaller singular values to zero, we can consider a part of the matrix 𝑆 that has the same number of ranks, rows and columns, and it works in the same way for the matrices 𝑈 and 𝑉, and finally we calculate the product of these matrices, which gives us the denoised image matrix.

Before explaining the FFT method of image denoising, let's take a look at a low pass filter definition.

### Low Pass Filter
A low-pass filter works in such a way that it passes the frequencies that are lower than the cutoff frequency set for it and weakens the rest of the frequencies outside this condition. To implement this filter, it is first necessary to Fourier transform the data we have and then in its frequency spectrum, based on the definite frequency value we have, keep the frequencies that are lower than this value and remove the frequencies outside this area and zero the Fourier transform values at these points. In the last step, in order to display the desired data in the format we had at the beginning (or image or audio signal, etc.), we must take the inverse Fourier transform and display the final and filtered data.

### FFT Method for Image Denoising 
Now, in order to denoise the given images, we must do the same. That is, we first take a two-dimensional Fourier transform from the matrix of our image and then, based on the radius we have determined, pass the Fourier transform values of the image both in the direction of the rows and columns of its frequency spectrum by this radius and zero the rest of the Fourier transforms. For better understanding, suppose the frequency spectrum of an image is as shown below:

![Screenshot (65)](https://user-images.githubusercontent.com/125180530/219781699-4f9fe6f1-7187-4534-a84c-d01ceb7438d0.png)

In this case, according to the radius that we have determined in order to determine what frequency range to pass, from both dimensions of this Fourier transforms, we pass the frequencies equal to that radius and remove the rest, which is approximately the shape of the image spectrum after applying this The changes will be as follows:

![Screenshot (67)](https://user-images.githubusercontent.com/125180530/219782318-bcfad6ee-2967-4d62-bd79-53e9cfedd7ca.png)

* Now, we write functions for denoising images with these two defined methods. 

* After denoising the images, we compare the results of both methods and we came to the conclusion that in this case, the FFT method is better as well.  
