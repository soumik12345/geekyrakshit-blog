---
toc: true
layout: post
description: OpenGL GameDev Log 5, The OpenGL Graphics Pipeline.
categories: [gamedev, visualstudio, c++, opengl, window]
title: OpenGL GameDev Log 5 The OpenGL Graphics Pipeline
image: images/opengl-logs/logo.png
---

In OpenGL, everything is basically is 3D space but our window is a 2D array of pixels. This means, OpenGL has to convert 3D coordinates into 2D pixel so that they can be displaed on our screen. This processing is managed by the **OpenGL Graphics Pipeline**. Although the graphics pipeline consists of several steps, it can be broadly categorized into two parts:

1. the part that transforms our 3D coordinates into 2D coordinates and
2. the part that transforms the 2D coordinates into actual colored pixels.

All of the steps in the graphics pipeline are highly specialized and can easily be executed in parallel, due to which, modern GPUs have thousands of small processing cores to quickly process your data within the graphics pipeline. The processing cores run small programs called **Shaders** on the GPU for each step of the pipeline.


<figure class="image">
    <center>
        <img src="https://raw.githubusercontent.com/soumik12345/geekyrakshit-blog/master/images/opengl-logs/log_5_1.png">
        <figcaption>The various steps in the OpenGL Graphics Pipeline. Source: <a href="https://learnopengl.com/">https://learnopengl.com/</a></figcaption>
    </center>
</figure>