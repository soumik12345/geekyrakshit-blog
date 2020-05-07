---
toc: true
layout: post
description: OpenGL GameDev Log 1, detailed instructions for setting up and linking GLFW with Visual Studio 2019.
categories: [gamedev, visualstudio]
title: OpenGL GameDev Log 1 Setting Up GLFW
image: images/opengl-logs/logo.png
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
7. Right-click on the project on Visual Studio and open `Properties` or simply hit `Alt+Enter` selecting the project on Visual Studio.

    <figure class="image">
        <center>
            <img src="{{site.baseurl}}/images/opengl-logs/log_1_2.png">
            <figcaption>Open Properties</figcaption>
        </center>
    </figure>

8. Make sure `Configuration` and `Platform` are set respectively to `All Configurations` and `Active(Win32)` respectively.
9. Select `C/C++` property from the list of `Configuration Properties` on the left side of the dialog box.

    <figure class="image">
        <center>
            <img src="{{site.baseurl}}/images/opengl-logs/log_1_3.png">
        </center>
    </figure>

10. Go to `General` under `C/C++` and edit the `Additional Include Directories` property. Here you should give the relative or dynamic path to the external input folder which is `$(SolutionDir)\Linking\GLFW\include`. Confirm and apply the change you made.
11. Go into `Linker` outside of `C/C++`, select `General` and edit the `Additional Library Directories` property, set it to `$(SolutionDir)\Linking\GLFW\lib`.
12. Now, go to `Input` under `Linker` and edit the `Additional Dependencies` directory. In the list, write down `opengl32.lib` and `glfw3.lib`. Apply everything.

    <figure class="image">
        <center>
            <img src="{{site.baseurl}}/images/opengl-logs/log_1_4.png">
            <figcaption>List the libraries in this manner</figcaption>
        </center>
    </figure>

13. Make a sanity check: inside a `cpp` file try to include `glfw3.h`, you should be getting autocomplete suggestions.
