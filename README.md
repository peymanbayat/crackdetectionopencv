# Crack detection using OpenCV

### Abstract
It has been seen that millions of dollars are being invested on highway/subway tunnel maintainance and restoration all over the world. This cost can be minimized if the detection of cracks will be found as earlier as possible. As the reparation process depends on the type of cracks, so we need to take actions for next steps how it would be repaired. It would be a very good decision to repair the cracks as earliar we find it. Initially we need to capture very transperant images of the roads/concrete infrastuctures. Cause detections will depend on that images. So any device that will be used to scan or capture images of the roads/concrete infrastuctures, that must be configured for picturing high resolution images. On those images, various image processing techniques are applied to extract crack information. Depending on these information, the images could be classified using some decision making algorithm. This procedure can be implemented on images acquired by any objects or vehicles carrying image sensing terminal, laser distance sensor, image storage and processing servers, central control system and speed sensor. The accuracy depends on the images quality and accurate capture.

### Introduction
Whenever we travel what we need at first is road safety. So if we can confirm that conditions of our highway is okay, then accidents will be decreased automatically. Since the highways are built, it can be seen the cracks or holes in the asphalt/concrete surface. As soon as we repair our cracks, our journey will be safe for sure. Most of cases the accidents happen due to the poor condition of the road.

In very modern countries, they have thousands of kilometers highways. It's very difficult to inspect these roads by manpower. So an efficient automatic detection of the road condition can be developed for making them safe.

These cracks of the highways can be classified into some types. Depending on those cracks, authority must take actions how those would have to repair. Initially it may need to detect the location of the cracks. To perform that, a visual inspection technique is needed to capture images of the roads and then to be analyzed.

So our ultimate goal is to develop a system that can be able to detect these cracks on the highways automatically.

### Methodology
Here the crack detection methodology can be classified into some following steps below:
1. Image capture
2. Image processing
3. Image Segmention
4. Feature extraction

#### Image capture
Any device can be installed on a vehicle zenith point or in a pole that is capable of capturing high resoluted imgaes of higways from any angle but focus should be perfect. If needed then the original images could be resized. Here are some examples of images on which we are going to detect cracks.

<img src="Input-Set/Cracked_01.jpg" width="420" height="250"> <img src="Input-Set/Cracked_07.jpg" width="420" height="250">

#### Image processing
All the steps in the processing section are being explained below. 

Firstly, the images is transformed in a new one in grayscale and blur. These make the images easier to visualize the processed images in next steps. 

<img src="Processed-Set/blur-1.jpg" width="420" height="250"> <img src="Processed-Set/blur-7.jpg" width="420" height="250">
<pre>              Blurred Image                                           Blurred Image</pre>

Logarithmic transformation is used to replace all the pixels values of an image with its logarithmic values. This transformation is used for image enhancement as it expands dark pixels of the image as compared to higher pixel values. So if we apply this method in an image having higher pixel values then it will enhance the image more and actual information of the image will be lost. Now after applying the log transformation in to our sample blurred images, they look like below.

<img src="Processed-Set/img_log-1.jpg" width="420" height="250"> <img src="Processed-Set/img_log-7.jpg" width="420" height="250">
<pre>           Log Transformed Image                                   Log Transformed Image</pre>

The bilateral filter also uses a Gaussian filter in the space domain, but it also uses one more (multiplicative) Gaussian filter component which is a function of pixel intensity differences. This method preserves edges, since for pixels lying near edges, neighboring pixels placed on the other side of the edge, and therefore exhibiting large intensity variations when compared to the central pixel, will not be included for blurring. So the sample logarithmic transformed images become as following after applying the bilateral filtering.

<img src="Processed-Set/bilateral-1.jpg" width="420" height="250"> <img src="Processed-Set/bilateral-7.jpg" width="420" height="250">
<pre>           Bilateral Filtered Image                           Bilateral Filtered Image</pre>

Canny edge detection is a technique to extract useful structural information from different vision objects and dramatically reduce the amount of data to be processed. It uses a multi-stage algorithm to detect a wide range of edges in images. 
Canny algorithm consists of three main steps:

1. Find the intensity gradient of the image: In this step the scale of the gradient vector is calculated for each pixel.
2. Non-maximum suppression: The aim of this step is to “thin” the edge to obtain a one-pixel width edge.
3. Threshold hysteresis: Finally, a two-step threshold hysteresis is applied in order to decrease the fake edges.

Now we apply canny algorithm to detect the crack edges in our bilateral filtered as following.

<img src="Processed-Set/edges-1.jpg" width="420" height="250"> <img src="Processed-Set/edges-7.jpg" width="420" height="250">
<pre>           Canny Edges Image                                   Canny Edges Image</pre>

Morphological transformations are some simple operations based on the image shape. It is normally performed on binary images. It needs two inputs, one is our original image, second one is called structuring element or kernel which decides the nature of operation. 

There are many different types of morphological filtering, but after analyzing the results, the best filter for this detection is the closing filter. Closing filter helps to fill minor gaps in the image making the main crack continuous and more detailed. It is useful in closing small holes inside the foreground objects, or small black points on the object. Closing filter is defined as a dilation followed by an erosion.

Here we go to apply the morphological closing operator onto our canny edges detected images.

<img src="Processed-Set/closing-1.jpg" width="420" height="250"> <img src="Processed-Set/closing-7.jpg" width="420" height="250">
<pre>           Morphological Closing Image                          Morphological Closing Image</pre>
