---
layout: post
title: cocos2d-x for linux
categories: cocos
tags: cocos linux
---

###  cocos2d-x for linux

---

cocos2d-x version : 3.8

---

#### step:

1. **get the source code**
	- sudo apt-get install git
	- git clone https://github.com/cocos2d/cocos2d-x.git
	- or you can download at   http://cn.cocos2d-x.org/download/

2. **init environment**
	- cd cocos2d-x/build
	- ./install-deps-linux.sh
	- python ../download-deps.py

3. **make code**
	- cmake ..
	- make

4. **Test run the sample**
	- cd /bin/cpp-tests
	- ./cpp-tests

---

#### some problems:

- if had not gcc ,then run:
	- sudo apt-get install build-essential

- **Could NOT find GLEW (missing: GLEW_INCLUDE_DIR GLEW_LIBRARY)**
	- Answer:
	- *sudo apt-get install glew-utils libglew-dev*
      if it still show error, "checking for module 'glfw3' --   package 'glfw3' not found
      CMake Error at cmake/Modules/FindPackageHandleStandardArgs.cmake:136 (message):" 
      see the link :
      http://stackoverflow.com/questions/17768008/how-to-build-install-glfw-3-and-use-it-in-a-linux-project


- **Could not find CURL (missing: CURL_LIBRARY CURL_INCLUDE_DIR)**
	- Answer:
	- sudo apt-get install libcurl4-openssl-dev
    
- **error: ld terminated with signal 9 [Killed]**
	- 被强制终止，内存不够（因为用的虚拟机，比较奇葩的问题）
    
- **g++: internal compiler error: Killed (program cc1plus)**
	- 内存不够





