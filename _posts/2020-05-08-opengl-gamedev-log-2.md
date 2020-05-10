---
toc: true
layout: post
description: OpenGL GameDev Log 2, detailed instructions for setting up and linking GLFW, GLEW, SDL and SFML with Xcode on MacOS.
categories: [gamedev, visualstudio, glfw, glew, sdl, sfml]
title: OpenGL GameDev Log 2 Setting Up Dependencies on MacOS
image: images/opengl-logs/logo.png
---
## OpenGL GameDev Log 2: Setting up Dependencies on MacOS

### GLFW

[GLFW](https://www.glfw.org/) is an Open Source, multi-platform library for OpenGL, OpenGL ES and Vulkan development on the desktop. It provides a simple API for creating windows, contexts and surfaces, receiving input and events.

### GLEW

[The OpenGL Extension Wrangler Library](http://glew.sourceforge.net/) or GLEW in short, is a cross-platform open-source C/C++ extension loading library. GLEW provides efficient run-time mechanisms for determining which OpenGL extensions are supported on the target platform. OpenGL core and extension functionality is exposed in a single header file. GLEW has been tested on a variety of operating systems, including Windows, Linux, Mac OS X, FreeBSD, Irix, and Solaris.

### SDL

Simple DirectMedia Layer (SDL) is a cross-platform software development library designed to provide a hardware abstraction layer for computer multimedia hardware components.

### SFML

Simple and Fast Multimedia Library (SFML) is a cross-platform software development library designed to provide a simple application programming interface (API) to various multimedia components in computers. It is written in C++ with bindings available for C, Crystal, D, Euphoria, Go, Java, Julia, .NET, Nim, OCaml, Python, Ruby, and Rust.

### Installation steps

GLFW is written in C and supports Windows, macOS, the X Window System and the Wayland protocol.

Following are the steps to set up dependencies with Xcode on MacOS:

1. Install **brew** on your system using `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"` if not already installed. Brew is a package installer for MacOS.
2. Installation instructions on your system for all the libraries are as follows:
    - `brew install glew`
    - `brew install glfw3`
    - `brew install sdl2`
    - `brew install sfml`
3. Open Xcode and create a new empty project. Make sure to set the language as **C++**.
4. Select the project, Go to `Build Settings` and look up `Search Paths`.

    <figure class="image">
        <center>
            <img src="{{site.baseurl}}/images/opengl-logs/log_2_1.png">
        </center>
    </figure>

5. Add to `Header Search Paths` the path `/usr/local/include`.
6. Now go to `Build Phases` and open up `Link Binary with Libraries`.
7. Now we need to add the respective libraries (`dylib` files). These are localed at `/usr/local/Cellar`.

    <figure class="image">
        <center>
            <img src="{{site.baseurl}}/images/opengl-logs/log_2_2.png">
        </center>
    </figure>

8. In order to validate the installation, use the following code. The code explanation and breakdown  will be provided in a later post.
    ```c++
    #include <iostream>

    #define GLEW_STATIC
    #include "GL/glew.h"

    #include "GLFW/glfw3.h"

    #include "SDL2/SDL.h"
    #include "SDL2/sdl_opengl.h"

    using namespace std;

    const GLint WIDTH = 800, HEIGHT = 600;

    int main() {
        glfwInit();

        glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 3);
        glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 3);
        glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);
        glfwWindowHint(GLFW_OPENGL_FORWARD_COMPAT, GL_TRUE);
        glfwWindowHint(GLFW_RESIZABLE, GL_FALSE);

        GLFWwindow* window = glfwCreateWindow(WIDTH, HEIGHT, "Test", nullptr, nullptr);

        int screenWidth, screenHeight;
        glfwGetFramebufferSize(window, &screenWidth, &screenHeight);

        if(window == nullptr) {
            cout << "Failed to create Window" << endl;
            glfwTerminate();
            return -1;
        }

        glfwMakeContextCurrent(window);

        glewExperimental = GL_TRUE;

        if(glewInit() != GLEW_OK) {
            cout << "Failed to initialize GLEW" << endl;
            return -1;
        }

        glViewport(0, 0, screenWidth, screenHeight);

        while(! glfwWindowShouldClose(window)) {
            glfwPollEvents();
            glClearColor(0.2f, 0.3f, 0.3f, 1.0f);
            glClear(GL_COLOR_BUFFER_BIT);
            glfwSwapBuffers(window);
        }
        
        cout << "Everything Succeeded";

        glfwTerminate();
        return 0;
    }

    ```

    This should produce a blank widow like the following:

    <figure class="image">
        <center>
            <img src="{{site.baseurl}}/images/opengl-logs/log_2_3.png">
        </center>
        <figcaption>Once you close this window, your console would say <code>Everything SucceededProgram ended with exit code: 0</code></figcaption>
    </figure>

9. In order to validate the SDL installation, use the following code. The code explanation and breakdown  will be provided in a later post.
    ```c++
    #include <iostream>

    #define GLEW_STATIC
    #include "GL/glew.h"

    #include "SDL2/SDL.h"
    #include "SDL2/SDL_opengl.h"

    using namespace std;

    const GLint WIDTH = 800, HEIGHT = 600;

    int main() {
        
        SDL_Init(SDL_INIT_EVERYTHING);
        
        SDL_GL_SetAttribute(SDL_GL_CONTEXT_PROFILE_MASK, SDL_GL_CONTEXT_PROFILE_CORE);
        SDL_GL_SetAttribute(SDL_GL_CONTEXT_MAJOR_VERSION, 3);
        SDL_GL_SetAttribute(SDL_GL_CONTEXT_MINOR_VERSION, 3);
        SDL_GL_SetAttribute(SDL_GL_STENCIL_SIZE, 8);
        
        SDL_Window* window = SDL_CreateWindow("Test", 0, 0, WIDTH, HEIGHT, SDL_WINDOW_OPENGL);
        
        SDL_GLContext context = SDL_GL_CreateContext(window);
        
        glewExperimental = GL_TRUE;
        
        if(glewInit() != GLEW_OK) {
            cout << "Failed to initialize GLEW" << endl;
            return -1;
        }
        
        glViewport(0, 0, WIDTH, HEIGHT);
        
        SDL_Event windowEvent;
        
        while(true) {
            if(SDL_PollEvent(&windowEvent)) {
                if(windowEvent.type == SDL_QUIT)
                    break;
            }
            glClearColor(0.1f, 0.2f, 0.3f, 1.0f);
            glClear(GL_COLOR_BUFFER_BIT);
            SDL_GL_SwapWindow(window);
        }
        SDL_GL_DeleteContext(context);
        SDL_DestroyWindow(window);
        SDL_Quit();
        
        cout << "Everything Succeeded" << endl;
        
        return 0;
    }
    ```

    This should produce a blank widow like the following:

    <figure class="image">
        <center>
            <img src="{{site.baseurl}}/images/opengl-logs/log_2_4.png">
        </center>
        <figcaption>Once you close this window, your console would say <code>Everything Succeeded Program ended with exit code: 0</code></figcaption>
    </figure>

10. In order to validate the SFML installation, use the following code. The code explanation and breakdown  will be provided in a later post.

    ```c++
    #include <iostream>

    #define GLEW_STATIC
    #include "GL/glew.h"

    #include <SFML/Window.hpp>

    using namespace std;
    using namespace sf;

    const GLint WIDTH = 800, HEIGHT = 600;

    int main() {
        
        ContextSettings settings;
        settings.depthBits = 24;
        settings.stencilBits = 8;
        settings.majorVersion = 3;
        settings.minorVersion = 3;
        settings.attributeFlags = ContextSettings::Core;
        
        Window window(VideoMode(WIDTH, HEIGHT, 32), "Test", Style::Titlebar | Style::Close, settings);
        
        glewExperimental = GL_TRUE;
        
        if(glewInit() != GLEW_OK) {
            cout << "Failed to initialize GLEW" << endl;
            return -1;
        }
        
        bool running = true;
        
        while(running) {
            Event windowEvent;
            while(window.pollEvent(windowEvent)) {
                if(windowEvent.type == Event::Closed) {
                    running = false;
                    break;
                }
            }
            glClearColor(0.3f, 0.2f, 0.1f, 1.0f);
            glClear(GL_COLOR_BUFFER_BIT);
            window.display();
        }
        
        window.close();
        
        cout << "Everything Succeeded" << endl;
        
        return 0;
    }
    ```

    This should produce a blank widow like the following:

    <figure class="image">
        <center>
            <img src="{{site.baseurl}}/images/opengl-logs/log_2_5.png">
        </center>
        <figcaption>Once you close this window, your console would say <code>Everything Succeeded Program ended with exit code: 0</code></figcaption>
    </figure>


### SOIL2

**SOIL2** is a fork of the Jonathan Dummer's [Simple OpenGL Image Library](http://www.lonesock.net/soil.html).

**SOIL2** is a tiny C library used primarily for uploading textures into OpenGL.
It is based on [stb_image](http://www.nothings.org/stb_image.c), the public domain code from Sean Barrett.

**SOIL2** extended stb_image to DDS files, and to perform common functions needed in loading OpenGL textures.

**SOIL2** can also be used to save and load images in a variety of formats (useful for loading height maps, non-OpenGL applications, etc.)

### Installation steps for SOIL2

1. Download the premake 5 (alpha) binaries for MacOS from [https://premake.github.io/download.html#v5](https://premake.github.io/download.html#v5) and unzip. It contains an executable file called `premake`.

2. `git clone https://github.com/SpartanJ/SOIL2`
3. Copy `premake` inside `soil2` repository.
4. `./premake xcode4`
5. Copy the `SOIL2.h` file from the soil source directory to your source directory and link it.
6. For sanity check, inlcude `SOIL2.h` in a `cpp` file and check whether autocompletion works for `SOIL` or not.