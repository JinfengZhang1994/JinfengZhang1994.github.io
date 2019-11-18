[TOC]

## nvidia显卡驱动
```bash
zjf@zjf-SYS-7048GR-TR:~$ nvidia-smi 
Sat Nov 16 19:40:49 2019       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 384.130                Driver Version: 384.130                   |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce GTX 1080    Off  | 00000000:82:00.0  On |                  N/A |
| 27%   29C    P8    11W / 180W |    509MiB /  8113MiB |     17%      Default |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|    0      1637      G   /usr/lib/xorg/Xorg                           257MiB |
|    0      2743      G   compiz                                       103MiB |
|    0      3169      G   fcitx-qimpanel                                 7MiB |
|    0     12484      G   .../Qt5.11.1/Tools/QtCreator/bin/qtcreator     2MiB |
|    0     20290      G   /opt/ros/kinetic/lib/rviz/rviz                 9MiB |
|    0     29522      G   ...uest-channel-token=17905391342246558518   126MiB |
+-----------------------------------------------------------------------------+
zjf@zjf-SYS-7048GR-TR:~$ lspci|grep -i nvidia
82:00.0 VGA compatible controller: NVIDIA Corporation GP104 [GeForce GTX 1080] (rev a1)
82:00.1 Audio device: NVIDIA Corporation GP104 High Definition Audio Controller (rev a1)
zjf@zjf-SYS-7048GR-TR:~$ sudo dpkg --list|grep nvidia-*
[sudo] password for zjf: 
ii  nvidia-384                                   384.130-0ubuntu0.16.04.2                              amd64        NVIDIA binary driver - version 384.130
ii  nvidia-opencl-icd-384                        384.130-0ubuntu0.16.04.2                              amd64        NVIDIA OpenCL ICD
ii  nvidia-prime                                 0.8.2                                                 amd64        Tools to enable NVIDIA's Prime
ii  nvidia-settings                              361.42-0ubuntu1                                       amd64        Tool for configuring the NVIDIA graphics driver

zjf@zjf-SYS-7048GR-TR:~$ cat /proc/driver/nvidia/version 
NVRM version: NVIDIA UNIX x86_64 Kernel Module  384.130  Wed Mar 21 03:37:26 PDT 2018
GCC version:  gcc version 5.4.0 20160609 (Ubuntu 5.4.0-6ubuntu1~16.04.12) 
zjf@zjf-SYS-7048GR-TR:~$ nvcc -V
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2016 NVIDIA Corporation
Built on Tue_Jan_10_13:22:03_CST_2017
Cuda compilation tools, release 8.0, V8.0.61
```
## cuda8.0
***
![](/home/zjf/Desktop/zjf_notebook/pics/cuda_install_1.png) 
![](/home/zjf/Desktop/zjf_notebook/pics/cuda_install_2.png) 
[安装教程](https://blog.csdn.net/QLULIBIN/article/details/80728355)

## opencv2.4.11
***
查看版本号命令：
```bash
pkg-config opencv --modversion
```
[安装教程](https://blog.csdn.net/liuxiaodong400/article/details/81089058)
其中cmake选项改为：
```bash
cmake \
    -D CMAKE_BUILD_TYPE=DEBUG \
    -D CMAKE_INSTALL_PREFIX=/usr/local/opencv342 \
    -D WITH_CUDA=ON \
    -D WITH_CUBLAS=ON \
    -D CUDA_FAST_MATH=ON \
    -D WITH_CUFFT=ON \
    -D WITH_NVCUVID=ON \
    -D WITH_V4L=ON \
    -D WITH_LIBV4L=ON \
    -D WITH_OPENGL=ON \
    -D WITH_FFMPEG=ON \
    -D INSTALL_C_EXAMPLES=ON \
    -D BUILD_EXAMPLES=ON \
    .. 
```
## caffe
***
[安装教程](https://blog.csdn.net/u011511601/article/details/80109122)
### make all -j8报错
**error-1：**
```bash
caffe/proto/caffe.pb.h: No such file or directory
```
解决方法： 用protoc从caffe/src/caffe/proto/caffe.proto生成caffe.pb.h和caffe.pb.cc，具体命令如下：
进入到CAFFE_ROOT/src/caffe/proto/目录：
```bash
protoc --cpp_out=CAFFE_ROOT/include/caffe/ caffe.proto
```
**error-2:**
```bash
fatal error: leveldb/db.h: No such file or directory
```
解决方法：[https://blog.csdn.net/muyeluo123/article/details/100917291]()
[升级cmake版本](https://blog.csdn.net/xiekaikaibing/article/details/80135834)

**error-3:**
```bash
fatal error: lmdb.h: No such file or directory
```
解决方法：[链接(整合了很多个缺少文件的报错)](https://blog.csdn.net/u012576214/article/details/68947893)
```bash
sudo apt install liblmdb-dev
```
**error-4:**
```bash
/usr/local/include/leveldb/status.h:57:39: error: ‘nullptr’ was not declared in this scope
   bool ok() const { return (state_ == nullptr); }
                                       ^
/usr/local/include/leveldb/status.h: In member function ‘leveldb::Status::Code leveldb::Status::code() const’:
```
解决方法：[更新gcc版本](https://www.cnblogs.com/feifanrensheng/p/9695749.html)
**error-5:**
```bash
LD -o .build_release/lib/libcaffe.so.1.0.0
/usr/bin/ld: cannot find -lcblas
/usr/bin/ld: cannot find -latlas
collect2: error: ld returned 1 exit status
Makefile:583: recipe for target '.build_release/lib/libcaffe.so.1.0.0' failed
make: *** [.build_release/lib/libcaffe.so.1.0.0] Error 1
```
解决方法：[https://blog.csdn.net/eastlhu/article/details/78533193]()
### sudo make runtest -j8报错
**error-1:**
```bash
/usr/include/c++/7/type_traits(539): error: expected a ">"
``` 
解决方法：
运行make all -j8时使用gcc,g++5版本
运行sudo make runtest -j8时使用gcc,g++7版本
## gcc/g++多版本共存/切换
[参考链接](https://blog.csdn.net/qq_31347869/article/details/94379302)

## valgrind工具使用
***
安装了valgrind-3.15.0

## latex工具安装
***
