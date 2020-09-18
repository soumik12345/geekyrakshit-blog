---
toc: true
layout: post
description: Implementation of "Efficient Graph-Based Image Segmentation" paper written by P. Felzenszwalb and D. Huttenlocher.
categories: [algebra, computervision, convolution, maths, python]
title: Efficient Graph-Based Image Segmentation
image: images/felzenszwalb_logo.png
---

In this article, we would be discussing the paper **[Efficient Graph-Based Image Segmentation](http://people.cs.uchicago.edu/~pff/papers/seg-ijcv.pdf)** by <a href="mailto:pff@ai.mit.edu">Pedro F. Felzenszwalb</a> from Artificial Intelligence Lab, Massachusetts Institute of Technology and <a href="mailto:dph@cs.cornell.edu">Daniel P. Huttenlocher</a> from Computer Science Department, Cornell University.

## What is Segmentation?

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

## The Idea

Observing the performance of the past methods of image segmentation, the objective of this paper has been to develop an alogorithm for image segmentation that

- captures perceptually important regions that reflect global aspect.
- runs efficiently at near linear time complexity, $$O(n * log(n))$$ in this case.

The idea proposed by Felzenszwalb and Huttenlocher is based on selecting edges from a graph, where each pixel corresponds to a node in the graph, and certain neighboring pixels are connected by undirected edges such that weights on each edge measure the dissimilarity between pixels. However, unlike the classical methods that predate this paper, this technique adaptively adjusts the segmentation criterion based on the degree of variability in neighboring regions of the image. This results in a method that, while
making greedy decisions, can be shown to obey certain non-obvious global properties. The adaptive criteria is defined as follows:

<blockquote>There is a boundary between two adjacent regions C<sub>i</sub> and C<sub>j</sub>, i.e,
Variation across C<sub>i</sub> and C<sub>j</sub> is greater than variation within C<sub>i</sub> or C<sub>j</sub> individually.</blockquote>

<figure class="image">
    <center>
        <img src="{{site.baseurl}}/images/felzenszwalb/felzenszwalb_3.png">
    </center>
</figure>

## Problem Formulation

Let $$G=(V, E)$$ be an undirected graph such that,

- $$v_{i} \epsilon V$$: set of vertices or pixels in the image to be segmented.
- $$e = (v_{i}, v_{j}) \epsilon E$$: set of edges corresponding to pairs of neighbouring vertices or pixels.
- Each edge $$e = (v_{i}, v_{j}) \epsilon E$$ has a weight $$w(v_{i}, v_{j})$$ denoting the dissimilarity between v<sub>i</sub> and v<sub>j</sub>.

$$S$$ is a segmentation of a graph G such that $${G}' = (V, {E}')$$ where $${E}' \subset E$$.
$$S$$ divides $$G$$ into $${G}'$$ such that it contains distinct components (or regions) $$C$$.

### Graph Representation

Let an image consist of pixels from P1 to P20.

<div class="mxgraph" style="max-width:100%;border:1px solid transparent;" data-mxgraph="{&quot;highlight&quot;:&quot;#0000ff&quot;,&quot;nav&quot;:true,&quot;resize&quot;:true,&quot;toolbar&quot;:&quot;zoom layers lightbox&quot;,&quot;edit&quot;:&quot;_blank&quot;,&quot;xml&quot;:&quot;&lt;mxfile host=\&quot;app.diagrams.net\&quot; modified=\&quot;2020-09-18T07:38:57.222Z\&quot; agent=\&quot;5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/85.0.4183.102 Safari/537.36\&quot; etag=\&quot;1VdCmRGr3K3VReG4K-48\&quot; version=\&quot;12.9.7\&quot; type=\&quot;device\&quot;&gt;&lt;diagram id=\&quot;OjWp4HWtmnEIbqeM9SzM\&quot; name=\&quot;Page-1\&quot;&gt;zdlNa4MwHAbwT+OxYIxWe23XbTAKAxk7jlAzlamRmE67T790JrY2KWyHkf+lmMf40p8lPFgPb+rhgZO22LGMVl7gZ4OH77wgiHEiP0/BcQyiAI9BzstsjNA5SMsvqkJfpYcyo91somCsEmU7D/esaehezDLCOevn095ZNb9qS3JqBOmeVGb6WmaiGNMk8s/5Iy3zQl8Z+WpPTfRkFXQFyVh/EeGthzecMTFu1cOGVic77TIed39j73RjnDbiNwdEu+QjjmjbPtUvixTxQ/NWLNRZPkl1UF/4WUWdOGqDvigFTVuyP417+Zg9vC5EXckRkpuka0f593Kg8mJrdU7KBR1u3iyaCORPh7KaCn6UU/QBWk39bEI17C+egYqKC36dEfXU8+nEZxi5oWz+4BSYTgEEp8CH5YRNJwzCKYHlFJpOIQQnvITlFJlOEQSnMITltDSdlhCcrtfxaewKKjahYghQ1wu5c6jEhEpAQCXAoFYm1AoC1PVS7hxKV/pZ2fQhUF2v5u6pbL0cZDGf1i1nVJZqrjNYS7p7Kks7RyDruXsqS0FHIBu6eypLR0cgS7p7KktNRyB7+mTgjMpS1BHIpu6eylLVEciu7p7KUtYRyLbunEovCLNXniDb+j9SyeH5Bf3Pvot/OfD2Gw==&lt;/diagram&gt;&lt;/mxfile&gt;&quot;}"></div>
<script type="text/javascript" src="https://app.diagrams.net/js/viewer.min.js"></script>