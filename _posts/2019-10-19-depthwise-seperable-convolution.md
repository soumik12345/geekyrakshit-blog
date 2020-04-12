---
toc: true
layout: post
description: Many modern CNN architectures such as Xception and Mobilenet make use of Depthwise Seperable Convolution to make them fast enough to run on mobile devices
categories: [algebra, cnn, computervision, convolution, convolutionaneuralnetwork, datascience, DeepLearning, depthwiseseperableconvolution, dnn, embeddeddevices, google, mathematics, maths, mobiledevices, mobilenet, multimodealnetwork, neural-networks, plotly, python, xception]
title: Depthwise Separable Convolutions in Deep Learning
---
# Depthwise Separable Convolutions in Deep Learning

The Convolution operation is a widely used function in Functional Analysis, Image Processing Deep Learning. The convolution operation when applied on two functions f and g, produces a third function expressing how the shape of one is modified by the other. While it is immensely popular, especially in the domain of Deep Learning, the vanilla convolution operation is quite expensive computationally. Modern Neural Network architectures such as [**Xception**](https://arxiv.org/abs/1610.02357) and [**MobileNet**](https://arxiv.org/abs/1704.04861) use a special type of Convolution called **Depthwise Separable Convolution** to speed up training and inference, especially on Mobile and Embedded Devices.

## The Vanilla Convolution Operation

The convolution function can be mathematically defined as the following:

$$(f \circledast g)(t) = \int_{- \infty}^{\infty} f(\tau) g(t - \tau) d\tau$$

For all non-negative values of t (i.e, for all values of t such that `t ∈ [0, ∞)` ), we could truncate the limits of integration resulting in,

$$(f \circledast g)(t) = \int_{0}^{t} f(\tau) g(t - \tau) d\tau$$

It can also be defined as the overlap of two functions f and g as one slides over the other, performing a sum of products.

<figure class="image">
    <center>
        <img src="{{site.baseurl}}/images/dsc/img_1.gif">
        <figcaption>Source: <a href="https://en.wikipedia.org/wiki/Convolution">https://en.wikipedia.org/wiki/Convolution</a></figcaption>
    </center>
</figure>

<figure class="image">
    <center>
        <img src="{{site.baseurl}}/images/dsc/img_2.gif">
        <figcaption>Convolution as Sum of Products. Source: <a href="https://towardsdatascience.com/intuitively-understanding-convolutions-for-deep-learning-1f6f42faee1">https://towardsdatascience.com/intuitively-understanding-convolutions-for-deep-learning-1f6f42faee1</a></figcaption>
    </center>
</figure>

## Computational Complexity of Convolution

In order to decide the computational complexity of the convolutional operation, we would count the number of multiplication operations for a convolution. This is because the Binary Addition of two numbers may be performed in a single clock cycle using two registers with the inputs latched and a bunch of combinatorial logic gates. Binary multiplication, however, requires successive shift and addition operations which must be performed as many times as there are bits in the multiplier and is thus a more expensive operation.

Let us consider an input volume of the dimension ($$D_{V}$$, $$D_{V}$$, N) where $$D_{V}$$ is the height and width of the volume and `N` is the number of channels. In the case of a standard RGB image `N = 3` and for a gray-scale image `N = 1`.

<figure class="image">
    <center>
        <img src="{{site.baseurl}}/images/dsc/img_3.png">
    </center>
</figure>

Let us convolve V with a tensor of shape ($$D_{V}$$, $$D_{V}$$, N) or N tensors with the shape ($$D_{K}$$, $$D_{K}$$) which results in a volume `G` of shape ($$D_{G}$$, $$D_{G}$$, N).
