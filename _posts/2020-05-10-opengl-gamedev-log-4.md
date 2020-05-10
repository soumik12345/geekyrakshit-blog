---
toc: true
layout: post
description: OpenGL GameDev Log 4, step by step guide for creating a window.
categories: [gamedev, visualstudio, c++, glfw, glew, window]
title: OpenGL GameDev Log 4 Creating a Window
image: images/opengl-logs/logo.png
---

## Anatomy of the programm

1. Create a header file in your project called `libs.h` and a C++ source file called `main.cpp`.

    <figure class="image">
        <center>
            <img src="{{site.baseurl}}/images/opengl-logs/log_4_1.png">
        </center>
    </figure>

2. Now import the necessary libraries in the header file.

    ```c++
    #pragma once

    #include<iostream>

    #include<glew.h>
    #include<glfw3.h>

    #include<glm.hpp>
    #include<vec2.hpp>
    #include<vec3.hpp>
    #include<vec4.hpp>
    #include<mat2x2.hpp>
    #include<mat3x3.hpp>
    #include<mat4x4.hpp>
    #include<gtc/matrix_transform.hpp>
    #include<gtc/type_ptr.hpp>

    #include<SOIL2.h>
    ```

3. include `"libs.h"` in `main.cpp`.

4. The anatomy of the main program is going to be the following:

    ```c++
    #include "libs.h"

    using namespace std;


    int main() {

        //////////////////////
        // Initialize GLFWW //
        //////////////////////

        /////////////////////
        // Create a Window //
        /////////////////////

        /////////////////////
        // Initialize GLEW //
        /////////////////////

        ///////////////
        // Main Loop //
        ///////////////

        /////////
        // End //
        /////////

        return 0;
    }
    ```