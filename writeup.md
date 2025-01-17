# **Traffic Sign Recognition** 

## Writeup Template

---

**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report

## Rubric Points

### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

You're reading it! and here is a link to my [project code](https://github.com/davidsosa/CarND-Traffic-Sign-Classifier-Project/blob/master/Traffic_Sign_Classifier.ipynb)

### Data Set Summary & Exploration

#### 1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

Loaded dataset. It already contained a separate validation set file, valid.p, so there
was no need to use sklearn to separate the dataset to a test set as suggested by the video 

Number of training examples = 34799

Number of validation examples = 4410

Number of testing examples = 12630

Image data shape = (32, 32, 3)

Number of classes = 43

#### 2. Include an exploratory visualization of the dataset.

No visualisation included

### Design and Test a Model Architecture

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

The only pre-processing I did was the MaxMin scaling applied one of the earlier assignments. This made a big difference when
analyzing the accuracy. I additionally tried to to convert to grayscale but I could not get the dimensions for the CovNet right,
so I decided to move on. Unfortunately, I only read about the possibility of augmenting the data after I had done the evaluation
on the test set and could not make any more changes to the model. Next time I will be careful and read rubric carefully before
starting the project. 

####2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x3 RGB image   							| 
| Convolution 5x5     	| 1x1 stride, valid padding, outputs 28x28x12 	|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 14x14x12 				|
| Convolution 5x5	    | 1x1 stride, valid padding, outputs 10x10x32      									|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 14x14x12 				|
| Fully connected		|       Input = 800, Output = 120  									|
| Dropout		|       probability = 0.50
| Fully connected		|       Input = 120, Output = 84  									|
| RELU					|												|
| Fully connected		|       Input = 84, Output = 43  									|


#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.


#### 4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* training set accuracy of: **99.4%**
* validation set accuracy of: **95.9%** 
* test set accuracy of: **94.1%**

If an iterative approach was chosen:
* What was the first architecture that was tried and why was it chosen?

Covnets should be useful when recognizing examples where the closeness of features matters.
Images are a perfect example of this. 

The first tried architecture was:

LeNet 

* What were some problems with the initial architecture?

I think the initial LeNet architecture (the one used for the MNIST charactes) was in a sense too 'broad'.
That is to say it was designed to work well with simple features.   


* How was the architecture adjusted and why was it adjusted? Typical adjustments could include choosing a different model architecture, adding or taking away layers (pooling, dropout, convolution, etc), using an activation function or changing the activation function. One common justification for adjusting an architecture would be due to overfitting or underfitting. A high accuracy on the training set but low accuracy on the validation set indicates over fitting; a low accuracy on both sets indicates under fitting.


* Which parameters were tuned? How were they adjusted and why?
Learning rate was increased to r=0.004 since this yielded better accuracy in the validation set. 
For the dropout rate I didn't really tune since I saw that the addition of dropout already increased
the accuracy quite a bit. Now that I observe there is some overfitting, maybe a higher dropout rate could have
improved this. 

* What are some of the important design choices and why were they chosen?
For example, why might a convolution layer work well with this problem?
How might a dropout layer help with creating a successful model?

If a well known architecture was chosen:

* What architecture was chosen?

LeNet

* Why did you believe it would be relevant to the traffic sign application?

Covnets should be useful when recognizing examples where the closeness of features matters.
Images are a perfect example of this. 

* How does the final model's accuracy on the training, validation and test set provide evidence that the model is working well?

I think the model is working well judging by reported accuracies. However I have identified a couple of things I could have done
to improve it even further that I was not able to do due to time constraints:

- Modify dropout rate since we have overfitting
- Augment the data by rotating it, etc.
- reduce the size of the filters  
- turn RGB to grayscale 


### Test a Model on New Images

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are five German traffic signs that I found on the web:

The images that may be difficult to classify are the one that have an angle and are far away. I would say
the hardest to classify are the roundabout and the pedestrian sign.

<img src="./my_images/nopassing.jpg" width="80"> <img src="./my_images/generalcaution.jpg" width="80"> <img src="./my_images/stopsign.jpg" width="80"> 

<img src="./my_images/pedestrian.jpg" width="80"> <img src="./my_images/roundabout.jpg" width="80">


#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| No Passing      		| No Passing   									| 
| General Caution     		| General Caution 										|
| Stop Sign			| Stop Sign
| Pedestrian Crossing 		| Traffic Signals					 				|
| Roundabout			| Roundabout      							|


The model was able to correctly guess 4 of the 5 traffic signs, which gives an accuracy of 80%.
I am not sure if this compares favorable with the test accuracy since the data sample is too small. But I would say
it is good since the Pedestrian crossing image looks difficult to classify (it is too far and on an angle) 

#### 3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

For all the images except for the pedestrian image, the top softmax probability was is very close to 1.

For the pedestrian image the probabilities are the following:

| Probability			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| .80      		| Traffic Signals   									| 
| .11     		| Go straingt or left 										|
| .08			| Keep right
| 0.008 		| General caution					 				|









