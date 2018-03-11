# CarND-Vehicle-Detection
Vehicle-Detection
# Histogram of Oriented Gradients (HOG)
1.Extracting Features
  In this project,features should imformative enough to distinguish between the car and the non-car.
  
  To make sure that all the fuction for feature extraction work properly, I first use two random-selected pictures in training dataset to   extract the features for car and not-car.Here are the image for the test result:
  
  The most of the code for feature extraction is contained in get_featue.py,which includes bin_saptial function, color_hist function, and   get_hog_feature ffunction to get the color histogram ,spatial feature, and HOG feature respectively.The first two feature are for 
  object's appearance and the third feature is for object's shape.
  
  However, the actual process function for feature extraction is performed by the function single_img_features,which takes only one input   image and a set of parameters from parameters.py, then return the feature analyzed for the image. To extract features for a list of 
  image,  extract_features will iterate the image list and return a list of features, one for each image.
  
2.Setting Parameters
  In order to select the proper parameter to enhance validation accuracy, I have tried many combinations of the parameters, it's a little 
  bit hard. After tuning many times, I found that YCrCb color space is more reliable than the others,it make the validation accuracy to 
  0.99.
  Althouth the use of all hog channel and the big spatial and hist bins really slow my pipeline process, it's in acceptable range based on   traing acuracy.Following is the paremeters in the parameters.py, which will be accessed anywhere in this project:
  
3.Training Classifier
  We have decided the feature fuction and the parameters will be used. Now, get the features from the dataset. Remember to define the
  sample size ensure the sample balance:
  
  We should standardize the feature vaector to have all feature in similiar range, enhancing reliability:
  
  Then, training the SVM and test the accuracy:
  
  
# Sliding Window Search
1.Describe how (and identify where in your code) you implemented a sliding window search. How did you decide what scales to search and how much to overlap windows?
  First, I created set of windows of different scale and stiched them together to get a window list, this is for the perpose of  
  different scale of classification for the car. But some cars in such a simple grid seems too small, some cars only be captured portion 
  of feature.
  Second, I have a implementation that increase the window size in every iteration of a row, and increase the overlap of windows. After   attempt, I can frame the car accurately, but it has many false positive and slow my detection process.
  
  Last, I apply the threshold and heat map method, it really reduce the false positive but still in catastrophy.I have tried many times   to take the different parameter combination,it still have many falsa positive in my detection process if I want to have accurate 
  detection of vehicle
  
2.Show some examples of test images to demonstrate how your pipeline is working. How did you optimize the performance of your classifier?
  The pipeline process is implemented in pipeline.py, actually process by the function pipeline_subprocess, which includes feature extraction, searching, classification and display the result. Following is the example images that show the initial sliding window, serch window, heatmap and the result image which apply the threshold method:
  
# Video Implementation
1.Provide a link to your final video output. 

2.Describe how (and identify where in your code) you implemented some kind of filter for false positives and some method for combining overlapping bounding boxes.
  I use the heatmap  to get detection result from the test image, and threslod the heatmap to reduce most of the false positive.
  The method is shown above of second point on the title slide window search.
  
# Disscussion
Briefly discuss any problems / issues you faced in your implementation of this project. Where will your pipeline likely fail? What could you do to make it more robust?
  In this project, I get frustrated on the parameter tuning. This is a little  tricker for me. Even now, I can't get the satisfying 
  result which remove all false positive and keep the detection window.
  Allthogh the false positive is so high, I also can get correct detection of vehicle on other video. Maybe it's not bad.
