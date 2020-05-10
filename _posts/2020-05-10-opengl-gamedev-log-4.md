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

        /////////////////////
        // Initialize GLFW //
        /////////////////////
        
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


## Initialize GLFW

Simply invoke `glfwInit();`.

```c++
#include "libs.h"

using namespace std;


int main() {

	/////////////////////
	// Initialize GLFW //
	/////////////////////
	glfwInit();
	
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

## Creating the Window

1. Define the dimensions of the window:

    ```c++
    const int WINDOW_HEIGHT = 720;
	const int WIDOWN_WIDTH = 1280;
    ```

2. Define the frame buffer sizes:

    ```c++
    int frameBufferHeight = 0, frameBufferWidth = 0;
    ```

5. Set a couple of properties for the window:
    
    1. Since we want to turns on all the moder OpenGL functionalities, we would say:

        ```c++
        glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);
        ```

    2. I want to use OpenGL version 4.4. In order to specify that, I would use the following settings:

        ```c++
        glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 4);
        glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 4);
        ```
    
    3. As of now we don't want our window to be resizable, so we would say:
    
        ```c++
        glfwWindowHint(GLFW_RESIZABLE, GL_FALSE);
        ```
    
    4. Since we want our game to be forward compatible or compatible with all subsequent versions of OpenGL, we would say:

        ```c++
        glfwWindowHint(GLFW_OPENGL_FORWARD_COMPAT, GL_TRUE);
        ```

4. Now we would create our window. We would be using the function `glfwCreateWindow()` that returns an object of type `GLFWwindow* window`. Following is the specification of the `glfwCreateWindow()` function:

    ```c++
    GLFWwindow* glfwCreateWindow(
        int 	        width,      // Window Width
        int 	        height,     // Window Heigh
        const char* 	title,      // The initial, UTF-8 encoded window title.
        GLFWmonitor* 	monitor,    // The monitor to use for full screen mode, or NULL for windowed mode.
        GLFWwindow* 	share       // The window whose context to share resources with, or NULL to not share resources.
    )	
    ```

    Now, we create a window using the following code snippet:

    ```c++
    GLFWwindow* window = glfwCreateWindow(
		WIDOWN_WIDTH, WINDOW_HEIGHT,
		"OpenGL Track", NULL, NULL
	);
    ```

    If you want to make the window fullscreen, you can use the function `glfwGetPrimaryMonitor()` to get the refernce to the primary monitor.

5. Now we need to prepare the FrameBuffer of the window. A **FrameBuffer** basically  is a portion of the RAM or Video Card containing a bitmap that drives a video display. We would actually need to retrieve the size, in pixels, of the framebuffer of the specified window. The function to do this is:

    ```c++
    glfwGetFramebufferSize(
		window,             // Window
		&frameBufferWidth,  // variable to store the width, in pixels, of the framebuffer, or NULL
		&frameBufferHeight  // variable to store the height, in pixels, of the framebuffer, or NULL
	);
    ```

6. Now we would set up our canvas. A canvas is the area of the window on which we can draw something. In this case, we would want to assign the whole framebuffer as our canvas. Hence we would say:

    ```c++
    glViewport(0, 0, frameBufferWidth, frameBufferHeight);
    ```

7. Now we want to make a context of the specified window current on the calling thread. A context must only be made current on a single thread at a time and each thread can have only a single current context at a time.

    ```c++
    glfwMakeContextCurrent(window);
    ```


## Initialize GLEW

1. We need to first set `glewExperimental = GL_TRUE;`.

2. Now we need to initialize GLEW. We can do that simply by calling `glewInit()` but we would also like to handle any error if GLEW initialization fail.

    ```c++
    if (glewInit() != GLEW_OK) {
		cout << "Error::main.cpp::GLEW Initialization Failed" << endl;
		glfwTerminate();
		return EXIT_FAILURE;
	}
    ```

## Main Loop

The **Main Loop** or the **Game Loop** consists of a loop inside which all the cool stuff actually takes place. The anatomy of the Main Loop consists of the following:

```c++
while (true) {

    // Input {
    //
    // }

    // Update {
    //
    // }

    // Draw {
    //	clear canvas
    //	update canvas	
    // }
}
```

Now comes the question that how long should the loop run (`while (true)` simply makes it an infinite loop) ? The answer is simple: till the window is kept open. So, we would modify the condition:

```c++
while (! glfwWindowShouldClose(window))
```

At this point in the program, if you attempt to close the window, you wouldn't be able to close it. So better not try it 😏.

<figure class="image">
    <center>
        <img src="{{site.baseurl}}/images/opengl-logs/acgan.png">
        <figcaption>If you have ignored my advice and already run the program, you can get rid of the unclosable window using the stop button in Visual Studio</figcaption>
    </center>
</figure>

