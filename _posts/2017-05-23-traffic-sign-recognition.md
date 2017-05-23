---
layout: single
title:  Traffic Sign Recognition
date:   2017-05-23
tags: convolutional-neural-network tensorflow self-driving-car
---
Yesterday, my 2nd project in [Self-Driving Car Nanodegree][carnd] finally passed! I'm not so proud of the fact that it's already missed the due date for 3 weeks; but I'm proud that I made noticeable improvements to the project each time I submit (3 submissions in total) and I won't learn so much if were to rush finishing it with quickfixes or tricks just to cover up.

### Introduction
The goal of this project is to train a model that can recognize German Traffic Signs. The models needs to reach >93% validation accuracy. Other requirements include having critical discussions about the dataset, models and results.

The overall flow of this project is: 
0. Read data, explore and visualize it
0. Preprocess data
0. Build the neural network
0. Train the model
0. Use the model to test on downloaded images
0. Analyze the results
0. Visualize neural network's internal states (Optional)

### Preparation
With the credits provided by the course, I launched a aws [g2.2xlarge][aws] instance with 32G storage. I used the Udacity provided carnd AMI so all the environments is ready once it's launched. I will use this machine to do all the hard training work instead of using my poor Macbook Pro. By the way, I have to open a support ticket to increase the limit (default 0) for launching GPU instances. I previously did it for us-west-2 but had to do it again for ap-southeast-2 (Sydney) as I find the response time using the latter region is way way better.

### Data
[GTSRB][gtsrb] has about 35,000 training images, 2500 for validation and 12,000 testing images. It has 43 classes and vary in sizes. I think it's only a subset since there're only 43 types of them. Udacity has scaled all the images into 32x32x3 and save them in pickle format so only 3 big files needed to be downloaded and restored. 

The labels for each image is 0-42 and the corresponding description is provided in a csv file. Here are the sample images from each one of the 43 classes (some are really dark)
![Training images sample][sample]

And here are distributions of each class in training, validation and test datasets.
![Data distribution][distribution]

The distribution is very skewed as we can see, which means we should balance it by some data augmentation techniques (which I hasn't done).

### Prepocessing
I only used the suggested normalization technique which is to substract 128 from each pixel and divided by 128 so that inputs fall between (-1, 1). The rational behind normalization is that gradient decent will converge quickly and more stable.

### Neural network architecture
I inherite the [LeNet][tflenet] neural network from previous lab since it provdes a good starting point (90% validation accuracy). The changes are mostly related to depth of feature maps since LeNet has only 1 channel while here we have 3.

The 1st convulation layer's output has 16 filters and 2nd has 32. The filter size are both 5x5 followed by 2x2 average pooling and then ReLu layer as activation function.

Then 1st full connection layer followed by a Dropout layer to prevent overfitting. After than another FC layer and finally output layer. Nothing special. Since it's a classification problem, I use softmax with cross entropy as loss function. Again, nothing special. 

I used TensorBoard to generate the graph below showing the architecture of my network. But I think TensorBoard could do amazing visualization like showing real time trend of traning/validation accuracy, as a dashboard. But to add all the 'summary' operations to enable that is kind of trivial, especially on a large network.
![Network Architecture][graph]

### Hyperparameters
Just the following 3. And it doesn't take me too long to setting with it because I inherite `BATCH_SIZE` and `rate` from previous lab.

    EPOCHS = 20
    BATCH_SIZE = 128
    rate = 0.001

### Results
Here is the result. My first 2 submission's test accuracy is around 84% and I thought maybe my network is too simple and planed to power it up. Then I found a stupid bug: I forgot to normaize the test data as I did for training and validation data.

    Training Accuracy = 0.995
    Validation Acurracy = 0.957
    Test Accuracy = 0.947

I knew some people manage to get over 99% test accuracy, which is really amazing. I'll try to improve it once I have some time.

### Test on download images
This part took me most of time. Not because it's hard but because I always forgot to check one of the rubics related to it, which is to discuss what features of the images might cause difficulty for your model. I spent a lot of time on images not suitable for this particular task. For example, at first I use images from the official websites, which is really silly because they probably are in training set and good quality. Then I use images from [Getty][getty], which are still good quality. Finally, I tried one suggestion given by my reviewer to use Google Street View then I found some 'good' distorted images which I can use for this task.

I think I'm too picky in choosing examples, wishing them to fall into my naratives. As long as I can make good educated guess, the task can be completed without that much effort.

### Visualizing internal states
The image below is an example. It's generated by drawing a grey scale picture using the activation output of the first convolutional layer. Not sure if it's just me or everyone, these kinds of 'internal state' kind of creeps me out. ( **WARNING**: Maybe [this][reveal_cnn] can better illustrate my feeling). Is that what's inside our brain?

It's actually very easy for this part as long as you know how to save and restore part of Tensorflow model.

### Final words
This is a good and interesting project to learn Tensorflow and CNN. But actually, the core part, which includes using Tensorflow to build the model is finished within 10% of total time (20 hours). Most of the time is spent getting data prepared, improving visualization, understand Tensorflow API (shape mismatch, save/restore variables etc) and discussing/analyzing results. I think I should be focused on the requirements next time.

And I hope in the future I can further improve the model using Keras to build a powerful model and try some data augumentation techniques. Also worth trying is using TensorBoard to track real time training accuracy.


[carnd]: https://www.udacity.com/course/self-driving-car-engineer-nanodegree--nd013
[aws]: https://aws.amazon.com/ec2/pricing/on-demand/
[gtsrb]: http://benchmark.ini.rub.de/?section=gtsrb&subsection=news
[tflenet]: https://github.com/tensorflow/models/blob/master/slim/nets/lenet.py
[getty]: http://www.gettyimages.com.au/


[sample]: https://github.com/sandyleo26/CarND-Traffic-Sign-Classifier-Project/raw/master/examples/sample.png
[distribution]: https://github.com/sandyleo26/CarND-Traffic-Sign-Classifier-Project/raw/master/examples/visualization.png
[graph]: https://github.com/sandyleo26/CarND-Traffic-Sign-Classifier-Project/raw/master/tensorboard.png
[internal]: https://github.com/sandyleo26/CarND-Traffic-Sign-Classifier-Project/raw/master/examples/featuremaps2.png
[reveal_cnn]: https://fananymi.files.wordpress.com/2015/03/reveals_cnn.png
