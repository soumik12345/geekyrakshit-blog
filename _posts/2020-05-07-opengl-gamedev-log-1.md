---
toc: true
layout: post
description: OpenKraft GameDev Log 1, getting started with Game Development using Java
categories: [gamedev, java, eclipse, lwjgl]
title: OpenKraft GameDev Log 1 - Getting started with the Project
image: images/opengl-logs/logo.png
---

OpenKraft is an OpenGL based Game Engine I sought out to write as basic OpenGL learning, which I eventually wish to expand to a Minecraft like voxel-based sandbox game engine. The idea behind this series is not to write a tutorial, but to maintain a development log for the project. We would begin with setting up our project.

Following are the steps to set up dependencies on MacOS and Eclise IDE:

1. Download [Light-Weight Java Game Library 2.9.1](https://www.youtube.com/redirect?v=Jdkq-aSFEA0&redir_token=VvmPJMAt4oYnswtqJ1y7X61VGbJ8MTU5MzM3ODY2OEAxNTkzMjkyMjY4&event=video_description&q=http%3A%2F%2Fsourceforge.net%2Fprojects%2Fjava-game-lib%2Ffiles%2FOfficial%2520Releases%2FLWJGL%25202.9.1%2Flwjgl-2.9.1.zip%2Fdownload).

2. Download [Slick-Utils JAR file](https://www.youtube.com/redirect?v=Jdkq-aSFEA0&redir_token=VvmPJMAt4oYnswtqJ1y7X61VGbJ8MTU5MzM3ODY2OEAxNTkzMjkyMjY4&event=video_description&q=http%3A%2F%2Fslick.ninjacave.com%2Fslick-util.jar).

3. Create a folder called `lib` to hold all our dependencies. Create 2 directories inside `lib` called `jars` and `natives`.

4. Move `lwjgl-2.9.1/jar/lwjgl.jar`, `lwjgl-2.9.1/jar/lwjgl_test.jar`, and `slick-util.jar` inside `libs/jars`.

5. Move the files under `lwjgl-2.9.1/native` inside `libs/natives`.

6. Under the project `OpenKraft`, copy and paste the `libs` directory and hit refersh in the IDE.

7. Right click on project > Build Path > Configure Build Path.

8. Go to Libraries > Add JARs > Add all the JAR files.

9. JRE System Library [JavaSE-1.8] > Native Library Location > Set to `libs/natives`.

10. Apply and Close.

11. We will start writing our Render Engine. Let's start by creating a package called `renderEngine`.

12. Under this there would be a class called `DisplayManager` which would manage the main display window of the game.

13. The constructor of a `DisplayManager` object takes in the title of the game, width of the window, height of the window and maximum frame-rate of the game.

    - `createDisplay()` function to create the display.
    - `updateDisplay()` function to update the display.
    - `isCloseRequested()` function to check if user has requested to close window or not.
    - `closeDisplay()` function to close the display.

14. Code for `renderEngine.DisplayManager`:

    ```java
    package renderEngine;

    import org.lwjgl.LWJGLException;
    import org.lwjgl.opengl.ContextAttribs;
    import org.lwjgl.opengl.Display;
    import org.lwjgl.opengl.DisplayMode;
    import org.lwjgl.opengl.GL11;
    import org.lwjgl.opengl.PixelFormat;

    public class DisplayManager {
        
        public int width, height, max_fps;
        public String title;
        
        public DisplayManager(String title, int width, int height, int max_fps) {
            this.title = title;
            this.width = width;
            this.height = height;
            this.max_fps = max_fps;
        }
        
        public void createDisplay() {
            
            ContextAttribs attributes = new ContextAttribs(3, 2);
            attributes.withForwardCompatible(true);
            attributes.withProfileCore(true);
            
            try {
                Display.setDisplayMode(new DisplayMode(this.width, this.height));
                Display.create(new PixelFormat(), attributes);
                Display.setTitle(this.title);
            } catch (LWJGLException e) {
                e.printStackTrace();
            }
            
            GL11.glViewport(0, 0, this.width, this.height);
            
            
        }
        
        public void updateDisplay() {
            Display.sync(this.max_fps);
            Display.update();
        }
        
        public void closeDisplay() {
            Display.destroy();
        }
        
        public boolean isCloseRequested() {
            return Display.isCloseRequested();
        }

    }
    ```

15. In order to test our engine, let's create a package called `engineTester`. Under this package we will create a sample game `Main.java`.

    ```java
    package engineTester;

    import renderEngine.DisplayManager;

    public class Main {

        public static void main(String[] args) {
            
            DisplayManager displayManager = new DisplayManager("OpenKraft", 1280, 720, 120);
            
            displayManager.createDisplay();
            
            while(!displayManager.isCloseRequested()) {
                displayManager.updateDisplay();
            }
            
            displayManager.closeDisplay();

        }

    }
    ```

    <figure class="image">
        <center>
            <img src="{{site.baseurl}}/images/opengl-logs/log_1.png">
            <figcaption>Result of executing the code</figcaption>
        </center>
    </figure>

**Corresponding Commit:** [https://github.com/soumik12345/OpenKraft/tree/13308a3b7c6b2d9614a848e5bd020f3c34e450c2](https://github.com/soumik12345/OpenKraft/tree/13308a3b7c6b2d9614a848e5bd020f3c34e450c2).