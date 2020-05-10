---
toc: true
layout: post
description: OpenGL GameDev Log 3, detailed instructions for setting up and linking SOIL2 with Visual Studio 2019 on Windows 10.
categories: [gamedev, visualstudio, soil2]
title: OpenGL GameDev Log 3 Setting Up and SOIL2 on Windows
image: images/opengl-logs/logo.png
---

## Instructions for setting up SOIL2

1. `git clone https://github.com/spartanj/soil2`
2. Download `premake-4.4-beta5-windows.zip` from [https://premake.github.io/download.html](https://premake.github.io/download.html) and unzip it.
3. Copy `premake4.exe` inside soil2.
4. Build soil2 binaries using `premake4.exe vs2012`.
5. Go inside `soil2\make\windows` and open up `SOIL2.sln` in Visual Stdio.
6. Build `soil2-static-lib` once for debug and then for release.
7. The directory for header files is `soil2\src\SOIL2` which is supposed to be updated in Visual Studio.
8. The lib directory to be linked is `soil2\lib\windows`.