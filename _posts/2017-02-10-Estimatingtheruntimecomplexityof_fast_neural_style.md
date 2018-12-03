---
layout: post
title: Running time complexity of fast-neural style algorithm
image: assets/images/style-transfer.jpg
featured: true
hidden: false
author: sheikirfanbasha
categories: [ machine-learning, style-ransfer, computer-vision ]
---


In this post we compute the running time complexity of the algorithm proposed in the paper 
**[Perceptual Losses for Real-Time Style Transfer](http://cs.stanford.edu/people/jcjohns/eccv16/)**. It will be helpful to decide on the required hardware or to estimate the number of days you will require to run your experiments.

# Quick calculation

The total number of computations for one forward pass of this algorithm is **20607** *million*. (*Refer below for detailed computation*)

Hence, if your computer is running on 2.2GHz porcessor. Then, total time required to finish these operations can be calculated as : 

Time required for forward pass = 20607 / 2200 = 9.36sec

Time required for one iteration/epoch = 2 * 9.36 = 18.72sec

Say, we are running for 40,000 iterations then time = 40,000 * 9.36 = 748800sec = 208hrs = 8.66 days approx.


# Basic Formulae

## Size of activation map

`oW = floor((padW * 2 + iW - kW) / dW) + 1`

where oW is the output width, padW is the horizontal padding, iW is the input width, kW is the kernel width and dW is the horizontal stride. In all the convolution layers where padding isn't explicitly specified, it is always considered a padding of floor(kW / 2). The same holds for the vertical dimension, with W replaced by H.

## Number of operations

`No.of operations = activation size x filter size x no.of filters`

## General

* 1 Giga = 1 billion
* 1 Giga(billion) = 1000 million
* 1 million = thousand thosands = 1000 * 1000

# Architecture along with computations

![runtimecomplexity](https://cloud.githubusercontent.com/assets/8801972/22853669/affeeb3c-f082-11e6-887c-80f5dc7aadbc.jpg)
