#  **Traffic Sign Classifier** 
## Udacity Self-Driving Car Nanodegree Project 3

**This project is to train and validate a model as below, so it can classify traffic sign images**

* Load the data set 
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images



[//]: # (Image References)

[image1]: ./images/img1.png "img1"
[image2]: ./images/img2.png "img2"
[image3]: ./images/img3.png "img3"
[image4]: ./images/img4.png "img4"
[image5]: ./images/img5.png "img5"
[image6]: ./images/img6.png "img6"
[image7]: ./images/img7.PNG "img7"
[image8]: ./images/img8.png "img8"
[image9]: ./images/img9.PNG "img9"
[image10]: ./images/img10.PNG "img10"
[image11]: ./images/img11.png "img11"
[image12]: ./images/img12.PNG "img12"
[image13]: ./images/img13.png "img13"
[image14]: ./images/img14.png "img14"

### Preparation of Environment


To run the code, following items was installed on my computer, 

* Anaconda 3
* Created an environment for TensorFlow 1.5
* Jupyter Notebook
* Numpy / Pandas / OpenCV / sklearn etc..

Copied following files from workspace to local drive
* 3 pickles to the folder of “/data”
* “Traffic_Sign_Classifier.ipynb” and “signnames.csv” to project folder

Also downloaded images of German traffic signs to the folder of “/test_images”


### Step 0: Load The Data

Open 3 pickle files (train.p, valid.p, test.p) and read into variables as summarized in Step 1.

### Step 1: Dataset Summary & Exploration

Dataset Summary

Print out the size of the data set

Variables | Data | Shape
----------|----------- |-----------
X_train | Features of training set | (34799, 32, 32, 3)
y_train | Label of training set | (34799,)
X_valid | Features of training set | (4410, 32, 32, 3) 
y_valid | Label of training set. | (4410,)
X_test | Features of training set | (12630, 32, 32, 3)
y_test | Label of training set. | (12630,)


Each image has a size of 32 by 32, below is several samples.
 
 ![alt text][image1]
 
#### Distribution/Histogram

There are 43 labels and the count of each label for 3 dataset are as below.

 ![alt text][image2]
 
#### Augmentation

The training set images are not evenly distributed, the first 18 labels have many more samples than the remaining labels. I did the augmentation of the training set to increase numbers of samples as below. 


 ![alt text][image3]
 
After augmentation, the training set looks like below.  I also did a comparison of accuracy by using original and augmentated training set. The augmentated method did incease the accuracy but not substantial.  Perphaps by making the distribution more evenly, the accuracy could be increased faster.

 ![alt text][image4]
 

### Step 2: Design and Test a Model Architecture

#### Pre-process the Data Set

Each image (32,32,3) was gray scaled into (32,32,1) by opencv function and then normalized ( pixel/255) which I found it is much faster alternative than using  the formula of “(pixel - 128)/ 128”.  

 ![alt text][image5]
  
Below is a comparison between these two methods.

 ![alt text][image6]
 
 
#### Model Architecture

The architecture is based on the LeNet provided by class while I made some adjustment on the output to help to increase the validation accuracy.

 ![alt text][image7]

#### Train, Validate and Test the Model

At beginning, I was struggling to increase the accuracy by adjusting parameter and did some comparison with different settings, such as already mentioned above, the formula for normalization, augmentation of training set. While later I found out the learning rate also play a key role to increase the accuracy. By using a rate of 0.0006, I can reach the target of 89% for validation set and 93% for training set.

 ![alt text][image8]
 
Below is comparison of different dropout rate (keep_prob). Though even with the same setting of all parameters, the result of accuracy could be different from each running of the code.  0.5 and 0.6 gave me a better result than 0.8

 ![alt text][image9]
 
### Step 3: Test a Model on New Images

#### Load and Output the Images

Following images was collected from web

 ![alt text][image10]
 
#### Predict the Sign Type for Each Image

Preprocessed these images in the same way for training set

 ![alt text][image11]
 
Predict the Sign type: the most difficult sign out of these new images is the speed limit sign of 70 km/H, sometime it is classifed as speed limit sign with other speed, like 20 or 40 or 60, etc.  Below is the result when it is classified as 20km/h
 
  ![alt text][image12]
 
#### Analyze Performance

I run the whole process many times and the performane is between 75% and 100% depending on if the signs of  “speed limit” and “No Passing” could be classified correctly or not.  The “No Passing” have a high chance to be classifed correctly. 

 ![alt text][image13]
 
#### Output Top 5 Softmax Probabilities For Each Image Found on the Web

All signs except “speed limit” and “No passing” have a very high possibilities for the first image, close to 100%. These two signs might not be classified correctly sometimes.

 ![alt text][image14]
 
 
### Discussion

This is a very challenging project for me since all these information are totally new to me, like CNN, tensorflow.  I studies the class material several time and understand more each time. The installation of tensorflow and got it running correctly on my laptop also took me a lot of time. It was so exiting when I saw the code is running and I realized that I learnt so much while working on this project. 

Then the next challenge is to increase the accuracy since the initial accuracy was 40% only. My mentor gave me valuable information and I also read many project writeup from other Udacity student to see how they achieve the 89% percentage requirement. Finally I can made it too. The whole learn curve is long and even painful but no pain, no gain, right?

The last challenge is the accuracy for the new images, especially the speed limit sign of 70 km/h which could be classified as speed limit of 20 km/h. At same time, I realized in the training set, some speed limit sign pictures are quite blur and they are not easy to be recognized even by human eyes either. It is amazing that CNN or the deep learning process could recognize these signs.

Again, I enjoyed the whole process and looking forward to the next project!

 
