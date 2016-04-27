---
layout: post
title: Java Note
categories: Java
tags: Java
---

##  Java Note

#### Java 概述

---
主要特性：__面向对象__， __跨平台（JVM）__

主要应用：

- web开发 （人人，去哪儿后台主要语言都是java）
- andriod开发 安卓平台上的app
- 客户端开发 （默认一般没有安装jvm，GUI库不够出色）
- 嵌入式开发 （难操作底层硬件灵活性小，jvm的缘故效率低。主要还是用汇编和C）

java版本：

- J2SE（Java Standard Edition) 标准版，客户端
- J2EE（Java Enterprise Edition） 企业版，web
- J2ME（Java Platform Micro Edition）微型版，嵌入式，移动平台。早期塞班上的java应用和游戏

---

####JVM（Java Virtual Machine)

---
JVM是实现__跨平台__的基础。是操作系统和上层之间的__中间件__

java源码编译后产生__.class文件__（字节码文件），JVM再负责把字节码文件翻译成各个平台不同的机器码。所以字节码文件都是一样的，不同的只是针对不同平台的jvm，翻译出平台适应的机器码。

JVM是用__C/C++__开发的，是编译后的机器码，不能跨平台，不同平台下需要安装不同版本的JVM。

---
####开发环境
---

#####JDK（Java Development Kit）
Java开发工具包, 运行java程序必需的依赖。

主要包括:

- JVM
- 基础类库
- 编译器
- 打包工具

#####环境变量

环境变量就是当告诉操作系统运行一个程序，除了当前路径，还应去哪些路径搜索。

- 用户变量：当前用户的环境变量
- 系统变量：对所有用户适用

java的环境变量：

- JAVA_HOME : JDK的安装路径
- Path : 加入java命令的搜索路径（`%JAVA_HOME%\bin`)
- CLASSPATH : 加载类的路径(`.;%JAVA_HOME%\lib` .表当前路径）

#####IDE（集成开发环境）
Eclipse（具体的使用技巧以后补充）

---