# What is it?
An android app runs caffe2 in real-time using previewed NDK camera image.

model: SqueezeNet  

fps: 6.8 on huawei mate 9

# I have seen apps running caffe, why redo it?
<0> I tried to create a ndk app where most of code related to caffe is in cpp.

<1> Integrated ndk camera with opencv and caffe2 in cpp.

<2> Tried to achieve better real-time performance.


# How to build?
<1> Android studio 2.3

<2> Android-21 and above

If compilation failed, try compile [google ndk camera sample](https://github.com/googlesamples/android-ndk/tree/master/camera).


# Which parts of program are in cpp?
<1> camera

<2> opencv

<3> caffe2 

# Be specific, what is written in cpp?
In this app, I tried to code almost everything in cpp.

<1> handle camera at low-level in cpp

<2> retrive raw image data in cpp.

<3> let opencv handle the raw data. (process raw data so that caffe can recognize it.)

<4> input image to caffe, and run caffe.

<5> when caffe is done, it's time to inform java, "hey java bro, result is ready, display it."

Java, of course, plays a crutial role in app lifecycle and user experience.

# Where did it run caffe?
In cpp/camera/ImageReader.cpp, ImageReader::RunCaffe() method if I remember correctly.

# Screenshot 
![screenshot](https://github.com/yge58/caffe2-opencv-ndkcamera/blob/master/device-2017-10-23-185701.png)

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
                               


Source code is based upon the following, and I am grateful to them.

[1] NDK sample code is from [Google NDK camera texture-view sample](https://github.com/googlesamples/android-ndk/tree/master/camera)

[2] Caffe2 C++ classification procedure is from [Caffe2 example](https://github.com/leonardvandriel/caffe2_cpp_tutorial/blob/master/src/caffe2/binaries/pretrained.cc)

[3] Caffe2 pretrained protobuf and libraries are from [AIcamera](https://github.com/bwasti/AICamera)

[4] The OpenCV libraries are from [OpenCV4Android](https://github.com/opencv/opencv/tree/master/samples/android)      

Issues and bugs (memory leaks, resource allocation and free, threads concurrency, how to balance workload between threadd and etc ... ) if you see any of them or have any improvement suggestions, please help me by filing as many issues as you want. I will be very grateful. 


