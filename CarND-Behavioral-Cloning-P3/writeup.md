# **Behavioral Cloning** 

[model.py]: ./model.py
[drive.py]: ./drive.py
[model.h5]: ./model.h5
[writeup.md]: ./writeup.md

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

---

**Behavioral Cloning Project**

The goals / steps of this project are the following:
* Use the simulator to collect data of good driving behavior
* Build, a convolution neural network in Keras that predicts steering angles from images
* Train and validate the model with a training and validation set
* Test that the model successfully drives around track one without leaving the road
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./examples/placeholder.png "Model Visualization"
[image2]: ./examples/placeholder.png "Grayscaling"
[image3]: ./examples/placeholder_small.png "Recovery Image"
[image4]: ./examples/placeholder_small.png "Recovery Image"
[image5]: ./examples/placeholder_small.png "Recovery Image"
[image6]: ./examples/placeholder_small.png "Normal Image"
[image7]: ./examples/placeholder_small.png "Flipped Image"

## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/432/view) individually and describe how I addressed each point in my implementation.  

---
### Files Submitted & Code Quality

#### 1. Submission includes all required files and can be used to run the simulator in autonomous mode

My project includes the following files:
* [model.py][model.py] containing the script to create and train the model
* [drive.py][drive.py] for driving the car in autonomous mode
* [model.h5][model.h5] containing a trained convolution neural network 
* [writeup.md][writeup.md] summarizing the results

#### 2. Submission includes functional code
Using the Udacity provided simulator and my [drive.py][drive.py] file, the car can be driven autonomously around the track by executing 
```sh
python3 drive.py model.h5
```

#### 3. Submission code is usable and readable

The [model.py][model.py] file contains the code for training and saving the convolution neural network. The file shows the pipeline I used for training and validating the model, and it contains comments to explain how the code works.

### Model Architecture and Training Strategy

#### 1. An appropriate model architecture has been employed

The model is based on the architecture of ["End to End Learning for Self-Driving Cars"](http://images.nvidia.com/content/tegra/automotive/images/2016/solutions/pdf/end-to-end-dl-using-px.pdf) (model.py lines 67-89) 

![alt text][image1]

The data is normalized in the model using a Keras lambda layer (code line 68), and the model includes RELU layers to introduce nonlinearity (code line 70-74).

#### 2. Attempts to reduce overfitting in the model

The model showed reasonable results with training loss and validation loss, so the additional layers were not added to handle the overfitting or underfitting.

#### 3. Model parameter tuning

The model used an adam optimizer, so the learning rate was not tuned manually (model.py line 87).

#### 4. Appropriate training data

Training data was chosen to keep the vehicle driving on the road. I personally collected data: center lane driving, recovering from the left and right sides of the road, driving counter-clock wise, and focusing on driving smoothly around curves.

### Model Architecture and Training Strategy

#### 1. Solution Design Approach

After collecting some data, I trained and simulated the model to see if the vehicle was driving successfully. Of course, it did not succeed at once. As the deep learning gets better with more good quality data, so I focused on getting more data than adjusting anything else, and then repeated the training and simulation task until the vehicle drives successfully. There were a few spots where the vehicle fell off the track. To improve the driving behavior in these cases, I collected more driving data in that spots.
At the end of the process, the vehicle is able to drive autonomously around the track without leaving the road.

#### 2. Final Model Architecture

The model architecture is as follows:

| Layer (type)         		   |     Output Shape	        					|   Param # |
|:--------------------------:|:----------------------------------:|:----------| 
| lambda 1 (Lambda)   		   | (None, 160, 320, 3)   							| 0         |
| cropping2d 1 (Cropping2D)  | (None, 65, 320, 3) 	              | 0         |
| conv2d 1 (Conv2d)	 				 | (None, 31, 158, 24)								| 1824      |
| conv2d 2 (Conv2d)	 				 | (None, 14, 77, 36)	 	 	   					| 21636     |
| conv2d 3 (Conv2d)	 				 | (None, 5, 37, 48)								  | 43248     |
| conv2d 4 (Conv2d)	 				 | (None, 3, 35, 64)	   							| 27712     |
| conv2d 5 (Conv2d)	 				 | (None, 1, 33, 64)								  | 36928     |
| faltten 1 (Flatten)        | (None, 2112)	                      | 0         |
| dense 1 (Dense)	         	 | (None, 100)       									| 211300    |
| dense 2 (Dense)	         	 | (None, 50)       									| 5050      |
| dense 3 (Dense)	         	 | (None, 10)       									| 510       |
| dense 4 (Dense)	         	 | (None, 1)        									| 11        |

#### 3. Creation of the Training Set & Training Process

To capture good driving behavior, I first recorded two laps on track one using center lane driving. Here is an example image of center lane driving:

![alt text][image2]

I then recorded the vehicle recovering from the left side and right sides of the road back to center so that the vehicle would learn to .... These images show what a recovery looks like starting from ... :

![alt text][image3]
![alt text][image4]
![alt text][image5]

Then I repeated this process on track two in order to get more data points.

To augment the data sat, I also flipped images and angles thinking that this would ... For example, here is an image that has then been flipped:

![alt text][image6]
![alt text][image7]

Etc ....

After the collection process, I had X number of data points. I then preprocessed this data by ...


I finally randomly shuffled the data set and put Y% of the data into a validation set. 

I used this training data for training the model. The validation set helped determine if the model was over or under fitting. The ideal number of epochs was Z as evidenced by ... I used an adam optimizer so that manually training the learning rate wasn't necessary.