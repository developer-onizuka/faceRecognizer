# faceRecognizer

# 1. Install face_recognition
```
$ sudo apt-get install python3-opencv
$ sudo apt-get install cmake libopenblas-dev liblapack-dev libjpeg-dev
$ sudo apt-get install python3-pip
$ sudo pip3 install face_recognition
```

# 2. Check if CUDA suppored
This is not used by CUDA lib. Some additional compiles is needed.
```
$ python3
Python 3.8.10 (default, Jun  2 2021, 10:49:15) 
[GCC 9.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import dlib
>>> dlib.__version__
'19.22.1'
>>> dlib.DLIB_USE_CUDA
False
```

# 3. Uninstall face_recoginition and dlib
```
$ sudo pip3 uninstall face_recognition
$ sudo pip3 uninstall dlib
```

# 4. Install gcc-6 which will be needed by compiling with cuDNN lib
```
$ sudo vi /etc/apt/sources.list
  # Adding below:
  deb http://dk.archive.ubuntu.com/ubuntu/ bionic main universe
$ sudo apt-get update
$ sudo apt-get install gcc-6 g++-6
```

# 5. Download and Install cuDNN if not install
https://developer.nvidia.com/rdp/cudnn-download
```
$ sudo dpkg -i libcudnn8_8.2.2.26-1+cuda11.4_amd64.deb 
$ sudo dpkg -i libcudnn8-dev_8.2.2.26-1+cuda11.4_amd64.deb
```

# 6. Install dlib with some compile options
```
$ git clone https://github.com/davisking/dlib.git
$ cd dlib
$ mkdir build
$ cd build
$ cmake .. -DDLIB_USE_CUDA=1 -DUSE_AVX_INSTRUCTIONS=1 -DCUDA_HOST_COMPILER=/usr/bin/gcc-6
$ cmake --build .
$ cd ..
$ sudo python3 setup.py install --set DLIB_USE_CUDA=1 --set USE_AVX_INSTRUCTIONS=1 --set CUDA_HOST_COMPILER=/usr/bin/gcc-6
$ pip3 list |grep dlib
```
# 7. Install face_recognition again
```
$ sudo pip3 install face_recognition
```
