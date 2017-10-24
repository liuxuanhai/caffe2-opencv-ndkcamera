
This demo aims at integrating Caffe2, OpenCV with Android at native level.

Source code is based upon the following and google ndk doc, I am deeply grateful to them,   

[1] The whole project is based on [Google NDK camera texture-view sample](https://github.com/googlesamples/android-ndk/tree/master/camera)

[2] The Caffe2 C++ classification procedure is from [Caffe2 example](https://github.com/leonardvandriel/caffe2_cpp_tutorial/blob/master/src/caffe2/binaries/pretrained.cc)

[3] The Caffe2 pretrained protobuf and related libraries are obtained from [AIcamera](https://github.com/bwasti/AICamera)

[4] The OpenCV libraries are obtained from [OpenCV4Android](https://github.com/opencv/opencv/tree/master/samples/android)      

# Preface

Hello, welcome. As title said, the demo deals directly with Android NDK camara c++ api. In this project, I tried to minimize java code interacting with Caffe. Efficiency is the goal.

The App is working, but far from finishing. Issues and bugs (memory leaks, resource allocation and free, multi-thread concurrency...)if you see any of them or have any improvement suggestions, please help me by filing as many issues as you want. I will be very grateful.

# Introduction

We love Caffe, OpenCV and Android, let's make an app including all three. 
Caffe, at its  core, is C++, OpenCV is C++ implemented as well. If we want real-time image classification on Android, it is natural to deal with NDK directly. That is, read image from ndk camera, pre-processing image using OpenCV, finally go through caffe.

JAVA is for user interface and app's lifecycle which are also important.

# Source Code Structure

  In texture-view,
           
              |__build
              |__build.gradle
              |__src
                   |__main
                         |__assets
                               |__squeeze_init_net.pb    (squeeze net architecture file)
                               |__squeeze_predict_net.pb (squeeze net pretrained weights)
                         |__cpp
                               |__caffe2  (caffe2 headers)
                               |__camera  (Android NDK native Camera API)
                               |__Eigen   (Eigen headers)
                               |__google  (protobuf headers)
                               |__opencv  (opencv headers)
                               |__opencv2 (opencv2 headers)
                               |__android_main.cpp   ( 1. contains all c++ files that are called from Java via JNI)
                                                     ( 2. handles all the native activities including camera, caffe, opencv.)
                               |__classes.h (Imagenet classes)
                               |__CMakeLists.txt     ( CMake )
                         |__Java
                               |__com__sample__textureview
                                                       |__ViewActivity.java (App's life cycle, UI)
                         |__libs
                               |__armeabi-v7a (This is the only ABI supported unfortunately)
                                            |__opencv (opencv4android libraries)
                                            |__(the rest libraries are copied from AICamera)
                         |__res
                         |__AndroidManifest.xml
                               

# Screenshot
-----------
![screenshot](https://github.com/yge58/caffe2-opencv-ndkcamera/blob/master/device-2017-10-23-185701.png)
