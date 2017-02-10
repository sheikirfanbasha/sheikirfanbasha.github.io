---
layout: post
title: Running time complexity of fast-neural style algorithm
---

![fast-neuralstyle](https://cloud.githubusercontent.com/assets/8801972/22820236/dbd7fd76-ef9b-11e6-97ad-43e9cc149c5d.jpg)

In this post we compute the running time complexity of the algorithm proposed in the paper 
**[Perceptual Losses for Real-Time Style Transfer](http://cs.stanford.edu/people/jcjohns/eccv16/)**


# Basic Formulae:

## Size of activation map:

`oW = floor((padW * 2 + iW - kW) / dW) + 1`

where oW is the output width, padW is the horizontal padding, iW is the input width, kW is the kernel width and dW is the horizontal stride. In all the convolution layers where padding isn't explicitly specified, it is always considered a padding of floor(kW / 2). The same holds for the vertical dimension, with W replaced by H.

## Number of operations:

`No.of operations = activation size x filter size x no.of filters`

# Architecture along with computations:

<table class="rich-diff-level-zero">
<thead class="rich-diff-level-one"> <tr> <th align="center">Layer</th> <th align="center">Activation Size</th> <th align="center">Number of operations</th> <th align="center">Total (in millions)</th> </tr> </thead>
<tbody class="rich-diff-level-one"> <tr> <td align="center">Input</td> <td align="center">3x256x256</td> <td align="center"></td> <td align="center"></td> </tr> <tr> <td align="center">Reflection padding</td> <td align="center">3x336x336</td> <td align="center"></td> <td align="center"></td> </tr> <tr> <td align="center">32x9x9 conv. stride 1</td> <td align="center">32x336x336</td> <td align="center">32x336x336x32x9x9</td> <td align="center">9364.04</td> </tr> <tr> <td align="center">64x3x3 conv. stride 2</td> <td align="center">64x168x168</td> <td align="center">64x168x168x64x3x3</td> <td align="center">1040.44</td> </tr> <tr> <td align="center">128x3x3 conv. stride 2</td> <td align="center">128x84x84</td> <td align="center">128x84x84x128x3x3</td> <td align="center">1040.44</td> </tr> <tr> <td align="center">Residual block; 128 filters<br>2 convs. with 3x3 filters, no padding</td> <td align="center">128x82x82<br>128x80x80</td> <td align="center">128x82x82x128x3x3 <br> 128x80x80x128x3x3</td> <td align="center">1935.20</td> </tr> <tr> <td align="center">Residual block; 128 filters<br>2 convs. with 3x3 filters, no padding</td> <td align="center">128x78x78<br>128x76x76</td> <td align="center">128x78x78x128x3x3 <br> 128x76x76x128x3x3 </td>
<td rowspan="4" align="center"> 5971.37</td>  </tr> <tr> <td align="center">Residual block; 128 filters<br>2 convs. with 3x3 filters, no padding</td> <td align="center">128x74x74<br>128x72x72</td> <td align="center">128x74x74x128x3x3 <br> 128x72x72x128x3x3</td>  </tr> <tr> <td align="center">Residual block; 128 filters<br>2 convs. with 3x3 filters, no padding</td> <td align="center">128x70x70<br>128x68x68</td> <td align="center">128x70x70x128x3x3 <br> 128x68x68x128x3x3</td>  </tr> <tr> <td align="center">Residual block; 128 filters<br>2 convs. with 3x3 filters, no padding</td> <td align="center">128x66x66<br>128x64x64</td> <td align="center">128x66x66x128x3x3 <br> 128x64x64x128x3x3</td>  </tr> <tr> <td align="center">64x3x3 conv. stride 1/2</td> <td align="center">64xx128x128</td> <td align="center">64x128x128x64x3x3</td> <td align="center">603.97</td> </tr> <tr> <td align="center">32x3x3 conv. stride 1/2</td> <td align="center">32x256x256</td> <td align="center">32x256x256x32x3x3</td> <td align="center">603.97</td> </tr> <tr> <td align="center">3x9x9 conv. stride 1</td> <td align="center">3x256x256</td> <td align="center">3x256x256x3x9x9</td> <td align="center">47.77</td> </tr> <tr> 
<td colspan="3" align="center">Total</td> <td align="center">20607.00</td>   </tr> </tbody>
</table>
