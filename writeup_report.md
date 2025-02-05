# **Traffic Sign Recognition** 

## Writeup

### You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

---

**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./Report_Images/Labels_Bar_Chart.png "Labels"
[image2]: ./Report_Images/Gray_Scale.png "Grayscaling"
[image3]: ./Report_Images/Learning_Curves.png "Learning Curve"
[image4]: ./Report_Images/Sample_Figs.png "Sample_Figs"
[image5]: ./Report_Images/Sample_Labelled.png "Sample_Labels"
[image6]: ./Report_Images/Performance.png "Predictor Performance"
[image7]: ./Report_Images/placeholder.png "Traffic Sign 4"
[image8]: ./Report_Images/placeholder.png "Traffic Sign 5"

## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

Here is a link to my [project code](https://github.com/wjs5211291/CarND-Traffic-Sign-Classifier-Project/blob/master/Traffic_Sign_Classifier.ipynb)

### Data Set Summary & Exploration

#### 1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is 32X32X3
* The number of unique classes/labels in the data set is 43

#### 2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. It is a bar chart showing how the data is distributed in each label, as you can see, the proportion of each label in train set is about equal to the proportion in both validation set and test set. 

![alt text][image1]

### Design and Test a Model Architecture

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

As a first step, I decided to convert the images to grayscale because the image feed into the model should have a depth of 1

Here is an example of a traffic sign image before and after grayscaling.

![alt text][image2]

As a last step, I normalized the image data because we need to have a mean value of zero and equal variance

I decided to generate additional data because the distribution of images is uneven

To add more data to the the data set, I used the following techniques because ... 

Here is an example of an original image and an augmented image:

![alt text][image3]

The difference between the original data set and the augmented data set is the following ... 


#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x1 grayscale image   					| 
| Convolution 3x3     	| 1x1 stride, valid padding, outputs 30x30x20 	|
| RELU					|												|
| Convolution 3x3		| 1x1 stride, valid padding, outputs 28x28x60 	|
| RELU					| 												|
| Max pooling			| 2x2 stride, outputs 14x14x60					|
| Convolution 3x3		| 1x1 stride, valid padding, outputs 12x12x160	|
|RELU					|												|
|Convolution 3x3		|1x1 stride, valid padding, outputs 10x10x150	|
|RELU					|												|
|Max pooling			|2x2 stride, outputs 5x5x150					|
|Fully connected		|input 3750, outputs 600						|
|RELU					|												|
|Drop out				|keep_prob = 0.5								|
|Fully connected		|input 600, outputs 200							|
|RELU					|												|
|Drop out				|keep_prob = 0.5								|
|LOGITS					|output 43										|
 


#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train the model, I used an AdamOptimizer optimizer,batch size=128, epochs = 20, learning rate = 0.001. I tried to reduce the learning rate, but the accuracy does not improve a lot.

#### 4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* training set accuracy of 0.998
* validation set accuracy of 0.969
* test set accuracy of 0.957

If an iterative approach was chosen:
* The first architecture that was tried is the LENET.
* The LENET has high efficiency but the validation accuracy is low than 0.9, which means that this model is underfitting.
* It may be that too few layers lead to underfitting，so I added two convolution lays. I added added two maxpool after relu. 
* To avoid overfitting, I added 2 dropout layers, and full connected layer for each.

This is the learning curve, here you can see how the training and validation accuracy. Because both values are high enough, so I think the model I am using is good enough.

![alt text][image3]

### Test a Model on New Images

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are 10 German traffic signs that I found on the web:

![alt text][image4] 


#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:
![alt text][image5]


The model was able to correctly guess 10 of the 10 traffic signs, which gives an accuracy of 100%. This compares favorably to the accuracy on the test set of 95.7%
It look like this classifier can give a perfect prediction if the size is square and size close to that of the training images, because when a image is not square, then the process of changing size will lose the information of features in the image, and this will lower down the accuracy of the classifier.

| Sign Labels       								|
|:-------------------------------------------------:|
|Road Work        									|
|Keep Right     									| 
|Priority Road										|
|No Passing for vehicle over 3.5 metric tons		| 
|Speed Limit(70km/h)								| 
|No Vehicles										|
|Keep Right											| 
|Speed Limit(50km/h)								|
|Bicycle Crossing									|
|End ofNo Passing for vehicle over 3.5 metric tons	|

 

#### 3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

The code for making predictions on my final model is located in the Ipython notebook.
![alt text][image6]

As you can see, the predictor has high confidence on most of the signs, just has a little bit uncertain on the sign of speed limit.

### (Optional) Visualizing the Neural Network (See Step 4 of the Ipython notebook for more details)
#### 1. Discuss the visual output of your trained network's feature maps. What characteristics did the neural network use to make classifications?


