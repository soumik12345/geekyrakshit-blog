---
toc: true
layout: post
description: OpenGL GameDev Log 1, setting Up GLFW
categories: [gamedev, visualstudio]
title: OpenGL GameDev Log 1 Setting Up GLFW
image: images/nearest-celeb-face/img_0.png
---
# OpenGL GameDev Log 1: Setting Up GLFW

[GLFW](https://www.glfw.org/) is an Open Source, multi-platform library for OpenGL, OpenGL ES and Vulkan development on the desktop. It provides a simple API for creating windows, contexts and surfaces, receiving input and events.

GLFW is written in C and supports Windows, macOS, the X Window System and the Wayland protocol.

Following are the steps to set up GLFW with Visual Studio 2019 on Windows 10:

1. Download 32 bit pre-compiled GLFW binaries for Windows from [https://www.glfw.org/download.html](https://www.glfw.org/download.html).


<figure class="image">
    <center>
        <img src="{{site.baseurl}}/images/opengl-logs/log_1_1.png">
        <figcaption>Download the 32 Bit pre-compiled binaries for Windows</figcaption>
    </center>
</figure>

2. Create an Empty project in Visual Studio 2019.
3. Unzip the GLFW binaries.
4. Create the following directory structure:
    ```
    Linking
    |
    -------GLFW
            |
            ----inlcude (copy contents of glfw-zip/inlcude)
            |
            ----lib (copy contents of files from glfw-zip lib-vc2019 folder)
    ```
5. Move the `Linking` folder to the project folder, keep it in the same location as the `sln` file.
6. Move the `dll` file (`dll` stands for **Dynamically Lined Libraries**) present in `Linking/GLFW/lib` to the root of the project where the source files will be present.
7. Right-click on the project on Visual Studio and open `Properties`.

<figure class="image">
    <center>
        <img src="{{site.baseurl}}/images/opengl-logs/log_1_2.png">
        <figcaption>Open Properties</figcaption>
    </center>
</figure>