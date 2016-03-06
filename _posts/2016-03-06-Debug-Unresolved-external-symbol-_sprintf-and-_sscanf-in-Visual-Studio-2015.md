---
layout: post
title: Debug：Unresolved external symbol _sprintf and _sscanf in Visual Studio 2015
categories: Debug_Windows
tags: Visual_Studio_2015 Debug
---

Recently, I was following the tutorial [OpenGL Essentials LiveLessons by Paul Varcholik](https://www.safaribooksonline.com/library/view/opengl-essentials-livelessons/9780133824360/). When I donwload [the sample source codes](https://bitbucket.org/pvarcholik/opengl-essentials-livelessons/overview), and played, no luck. I got errors like:
```C++
1>  Generating Code...
1>glfw3d.lib(context.obj) : error LNK2019: unresolved external symbol _sscanf referenced in function _parseGLVersion
1>glfw3d.lib(init.obj) : error LNK2019: unresolved external symbol _vsnprintf referenced in function __glfwInputError
1>LIBCMTD.lib(vsnprintf.obj) : error LNK2001: unresolved external symbol _vsnprintf
1>LIBCMTD.lib(vsnprintf.obj) : error LNK2001: unresolved external symbol __vsnprintf
1>F:\OpenGL\pvarcholik-opengl-essentials-livelessons-a0365eec59d9\source\Lesson1.2\bin\Debug\Lesson1_2.exe : fatal error LNK1120: 3 unresolved externals
```
