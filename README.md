####1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. Here is a template writeup for this project you can use as a guide and a starting point.

You're reading it!

###Histogram of Oriented Gradients (HOG)

####1. Explain how (and identify where in your code) you extracted HOG features from the training images.

I started by reading in all the vehicle and non-vehicle images. I extracted the HOG features for both cars and non car images with the following properties:
oreintation = 9
pix_per_cell = 8 # HOG pixels per cell
cell_per_block = 2 # HOG cells per block
hog_channel = "ALL" # Can be 0, 1, 2, or "ALL"

I have attached a sample of picture of HOG image of random car image.

####2. Explain how you settled on your final choice of HOG parameters.
The parameters which I tuned was

a) changed pix_per_cell to 4 and 16. The results wer better with pix_per_Cell to 8 and hence stuck with 8
b) cell_per_block also was tried to increase to 4. Better results were found at 2.
c) hog_channel was selected to "ALL" because better results were found at ALL than with a single channel


####3. Describe how (and identify where in your code) you trained a classifier using your selected HOG features (and color features if you used them).

The features which were used to train the classifer

a) Color histograms
b) Spatial Bins
c) HOG

The features are then normalized. The data is then divided to train data and test data. Then the features are fed to Linear SVM to train the SVM.

After the training, the svm accuracy is tested on test data. The accuracy of my SVM was around 99%.


###Sliding Window Search

####1. Describe how (and identify where in your code) you implemented a sliding window search. How did you decide what scales to search and how much to overlap windows?

The HOG is calculated for the entire image. A series of windows are defined for the entire image. For each window, the features (hogs, spatial bin and color hist) are calculated
and determined if that particular window is a car. If it is a car, then bounded box is drawn. The window is slid for the entire image and bounded boxes are drawn for car predictions. To smoothen the false positives, a heat map is calulcated and thresholded. The current values for threshold are 9 out of 10 images.

#####2. Show some examples of test images to demonstrate how your pipeline is working. What did you do to optimize the performance of your classifier?

There are some examples in python notebook. The pipeline was tested with different color spaces such as RGB, LUV, HSV and YcrCb. The best results were seen with LUV.



Video Implementation

####1. Provide a link to your final video output. Your pipeline should perform reasonably well on the entire project video (somewhat wobbly or unstable bounding boxes are ok as long as you are identifying the vehicles most of the time with minimal false positives.)
Link for final video attached. There are some false positives and some wobbly boxes but hopefully these should be ok.


####2. Describe how (and identify where in your code) you implemented some kind of filter for false positives and some method for combining overlapping bounding boxes.

I recorded the positions of positive detections in each frame of the video. From the positive detections I created a heatmap and then thresholded that map to identify vehicle positions. I then used scipy.ndimage.measurements.label() to identify individual blobs in the heatmap. I then assumed each blob corresponded to a vehicle. I constructed bounding boxes to cover the area of each blob detected.

####Issues in the project

a) The algorithm can be improved by removing false positives better.
b) Can use Udacity data set for data augmentation





