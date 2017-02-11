---
layout: post
title: Running time complexity of fast-neural style algorithm
---

![fast-neuralstyle](https://cloud.githubusercontent.com/assets/8801972/22820236/dbd7fd76-ef9b-11e6-97ad-43e9cc149c5d.jpg)

In this post we compute the running time complexity of the algorithm proposed in the paper 
**[Perceptual Losses for Real-Time Style Transfer](http://cs.stanford.edu/people/jcjohns/eccv16/)**

# Quick computation

The total number of computations for one forward pass of this algorithm is **20607** *million*.

Hence, if your computer is running on 2.2GHz porcessor. Then, total time required to finish these operations can be calculated as : 

Time required = 20607 / 

Time required =T<sub>f</sub>* 2 * N


# Basic Formulae:

## Size of activation map:

`oW = floor((padW * 2 + iW - kW) / dW) + 1`

where oW is the output width, padW is the horizontal padding, iW is the input width, kW is the kernel width and dW is the horizontal stride. In all the convolution layers where padding isn't explicitly specified, it is always considered a padding of floor(kW / 2). The same holds for the vertical dimension, with W replaced by H.

## Number of operations:

`No.of operations = activation size x filter size x no.of filters`

## General:

* 1 Giga = 1 billion
* 1 Giga(billion) = 1000 million
* 1 million = thousand thosands = 1000 * 1000

# Architecture along with computations:

| Layer        | Activation Size           | Number of operations                 | Total (in millions)  | 
|:-------------:|:------------------------:|:------------------------------------:|:-------------:|:-------------:|
| Input     | 3x256x256 |  | |
| Reflection padding      | 3x336x336      | |
| 32x9x9 conv. stride 1 | 32x336x336      | 32x336x336x32x9x9 | 9364.04 |
| 64x3x3 conv. stride 2 | 64x168x168      | 64x168x168x64x3x3 | 1040.44 |
| 128x3x3 conv. stride 2 | 128x84x84 | 128x84x84x128x3x3 | 1040.44 |
|Residual block; 128 filters<br>2 convs. with 3x3 filters, no padding | 128x82x82<br>128x80x80 |128x82x82x128x3x3 <br> 128x80x80x128x3x3 | 1935.20 |
|Residual block; 128 filters<br>2 convs. with 3x3 filters, no padding | 128x78x78<br>128x76x76 |128x78x78x128x3x3 <br> 128x76x76x128x3x3 <td rowspan=4> 5971.37
|Residual block; 128 filters<br>2 convs. with 3x3 filters, no padding | 128x74x74<br>128x72x72 |128x74x74x128x3x3 <br> 128x72x72x128x3x3
|Residual block; 128 filters<br>2 convs. with 3x3 filters, no padding | 128x70x70<br>128x68x68 |128x70x70x128x3x3 <br> 128x68x68x128x3x3
|Residual block; 128 filters<br>2 convs. with 3x3 filters, no padding | 128x66x66<br>128x64x64 |128x66x66x128x3x3 <br> 128x64x64x128x3x3|
|64x3x3 conv. stride 1/2| 64xx128x128 | 64x128x128x64x3x3 | 603.97|
|32x3x3 conv. stride 1/2 | 32x256x256 | 32x256x256x32x3x3 | 603.97|
|3x9x9 conv. stride 1 | 3x256x256 | 3x256x256x3x9x9 | 47.77
<td colspan=3>Total | 20607.00|
