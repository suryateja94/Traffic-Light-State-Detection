# Traffic-Light-State-Detection
A project developed for "CS-GY - 6643 Computer Vision and Scene Analysis" course @NYU Tandon

##Motivation


Self driving cars can make road travel cheaper and safer, that being said, the process of them becoming robust and reliable is still a few decades away. With Machine Learning applications being pervasive, the fact that they are computationally expensive and heavily dependant on pre processing doesn’t change. We have come up with a simple, yet effective solution to detect the state of a traffic light which will help the self driving car to make a decision about switching the engine on/off at the right time at a signal, utilizing fuel better and also contributing in small ways to make the environment a better place.


##Approach


In order to figure the state of a traffic light in an image, it is crucial to detect and confirm the presence of a traffic light and also identify the signal color to know if its in Red or Green state. As  detection  of  traffic  light  by  image  processing  techniques  alone  may  not give satisfactory results, we first look through the image with bounded intensity values for the colors Red ,Orange and Green. Once we find a match in color, we extract the region which is the area of interest. We then apply segmentation techniques to verify if a circular fit is possible. We also validate the same image by running canny and picking the strongest contours to see if the detected circular object is a part of a traffic signal.

####Color Matching -
For  each  image  we get as an input, the first step is to detect whether we get red, yellow or green. We set the intensity boundaries for each of the channel and try to see if the input image matches any of them. We have implemented three functions (one for each channel). Each of the three functions responds whether it was able to find the color in the image or not. If it does, it crops that part from the image for further analysis.


####Hough Circles -
In order to find the traffic lights in an image, it is crucial to find the shape of the detected match in the above step. The shape in consideration is a circle since traffic light casings are circular by default.  This  is  where  Hough  Circles  are  used  to  find  the  circular  shape based on a voting mechanism.  The  grayscale  image  undergoes  blurring  in  order  to  remove  noise  using  the Gaussian  Blur.  The  vote  is  accumulated  based  on  the  specified  parameters  such  as  the minimum,  maximum  radii  of  a  circle  and  the  threshold  for  the  number  of  votes  along  with 
specifying  the  gradients.  The  circular  elements  which  receive  the  majority  of  the  votes  will correspond to the traffic lights.


####Edge Detection and Shape fitting -
The captured image is passed as an input to the Canny() function defined in OpenCV. This step is  crucial  as  it  helps  us  decide  if  the  Hough  circle  found  is  indeed  that  of  a  traffic  light  by checking if the circle exists within the detected object. We used the findContours() function to find  a  closed  contour  and  approxPolyDP()  function  to  decide  if  a  contour  is  similar  to  a geometric shape with at least 4 vertices (assumption that a traffic signal box is of rectangular shape).


## Instructions to run project

1)   Install anaconda-navigator
2)   Open Jupyter
3)   Import the iPython Notebook(TrafficSignalStateDetection.ipynb)
4)   Run all the cells in the order
5)   For detection of traffic signal state in an image, use the ”Image Signal Detection” cell and put the path of input image
6)   For detection of traffic signal state in a video, use the “Video Signal Detection” cell and put the path of the video. Then use “Stitching all frames together for a Video” cell to create a new video detecting the state.


###Key Contributions:
Surya Teja Sharma - Gaussian Blur, Canny Edge Detection and Object Detection
Parth Shah - Color Bounding and Video Extraction and Stitching
Amartya Singh - Hough Transformation for Circle Detection


