---
layout: single
title:  Traffic Sign Recognition
date:   2017-05-23
tags: vim
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
With the credits provided by the course, I launched a aws [g2.2xlarge][aws] instance with 32G storage. I used the Udacity provided carnd AMI so all the environments is ready once it's launched. I will use this machine to do all the hard training work instead of using my poor Macbook Pro. By the way, I have to open a support ticket to increase the limit (default 0) for launching GPU instances. I previously did it for us-west-2 but had to do it again for ap-southeast-2 (Sydney) as I find the response using the latter region is way way better.

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

Then 1st full connection layer followed by a Dropout layer to prevent overfitting. After than another FC layer and finally output layer. Nothing special. Really.

Since it's a classification problem, I use softmax with cross entropy as loss function.

[carnd]: https://www.udacity.com/course/self-driving-car-engineer-nanodegree--nd013
[aws]: https://aws.amazon.com/ec2/pricing/on-demand/
[gtsrb]: http://benchmark.ini.rub.de/?section=gtsrb&subsection=news
[tflenet]: https://github.com/tensorflow/models/blob/master/slim/nets/lenet.py


[sample]: https://github.com/sandyleo26/CarND-Traffic-Sign-Classifier-Project/raw/master/examples/sample.png
[distribution]: https://github.com/sandyleo26/CarND-Traffic-Sign-Classifier-Project/raw/master/examples/visualization.png
