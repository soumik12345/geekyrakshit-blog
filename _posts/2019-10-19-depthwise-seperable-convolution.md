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
        <img src="{{site.baseurl}}/images/nearest-celeb-face/img_1.jpg">
        <figcaption>Source: <a href="https://en.wikipedia.org/wiki/Convolution">https://en.wikipedia.org/wiki/Convolution</a></figcaption>
    </center>
</figure>
