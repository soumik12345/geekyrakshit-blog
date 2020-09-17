---
toc: true
layout: post
description: Implementation of "Efficient Graph-Based Image Segmentation" paper written by P. Felzenszwalb and D. Huttenlocher.
categories: [algebra, computervision, convolution, maths, python]
title: Efficient Graph-Based Image Segmentation
image: images/felzenszwalb_logo.png
---

In this article, we would be discussing the paper **[Efficient Graph-Based Image Segmentation](http://people.cs.uchicago.edu/~pff/papers/seg-ijcv.pdf)** by <a href="mailto:pff@ai.mit.edu">Pedro F. Felzenszwalb</a> from Artificial Intelligence Lab, Massachusetts Institute of Technology and <a href="mailto:dph@cs.cornell.edu">Daniel P. Huttenlocher</a> from Computer Science Department, Cornell University.

## Segmentation

Before delving any further, let us try to understand a bit more about the task at hand. What exactly do we mean by image segmentation?

<blockquote>Image Segmentation can be defined as the task of partitioning a given image into a set of disjoint regions usually with a goal of simplifying the representation of the image into something that is more meaningful and easier to analyze.</blockquote>

<figure class="image">
    <center>
        <img src="{{site.baseurl}}/images/felzenszwalb/felzenszwalb_1.png">
    </center>
</figure>

It has been observed from past segmentation approaches that

- It's not adequate to assume that regions have nearly constant or slowly varying intensities.
- The determination of boundary between the regions cannot only use local decision criteria.

<figure class="image">
    <center>
        <img src="{{site.baseurl}}/images/felzenszwalb/felzenszwalb_2.png">
    </center>
</figure>

Observing the performance of the past methods of image segmentation, the objective of this paper has been to develop an alogorithm for image segmentation that

- captures perceptually important regions that reflect global aspect.
- runs efficiently with time complexity of $$O(n * log(n))$$.

The idea proposed by Felzenszwalb and Huttenlocher is based on selecting edges from a graph, where each pixel corresponds to a node in the graph, and certain neighboring pixels are connected by undirected edges such that weights on each edge measure the dissimilarity between pixels. However, unlike the classical methods that predate this paper, this technique adaptively adjusts the segmentation criterion based on the degree of variability in neighboring regions of the image. This results in a method that, while
making greedy decisions, can be shown to obey certain non-obvious global properties. The adaptive criteria is defined as follows:

<blockquote>There is a boundary between two adjacent regions C<sub>i</sub> and C<sub>j</sub>, i.e,
Variation across C<sub>i</sub> and C<sub>j</sub> is greater than variation within C<sub>i</sub> or C<sub>j</sub> individually.</blockquote>
