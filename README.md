# faceRecognizer

```
$ sudo apt-get install python3-opencv
$ sudo apt-get install cmake libopenblas-dev liblapack-dev libjpeg-dev
$ sudo apt-get install python3-pip
$ sudo pip3 install face_recognition

$ python3
Python 3.8.10 (default, Jun  2 2021, 10:49:15) 
[GCC 9.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import dlib
>>> dlib.__version__
'19.22.1'
>>> import face_recognition
>>> face_recognition.__version__
'1.2.3'

$ python3
Python 3.8.10 (default, Jun  2 2021, 10:49:15) 
[GCC 9.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import dlib
>>> dlib.DLIB_USE_CUDA
False


$ sudo vi /etc/apt/sources.list
  # Adding below:
  deb http://dk.archive.ubuntu.com/ubuntu/ bionic main universe

$ sudo apt-get update
$ sudo apt-get install gcc-6 g++-6




$ git clone https://github.com/davisking/dlib.git
$ cd dlib
$ mkdir build
$ cd build
$ cmake .. -DDLIB_USE_CUDA=1 -DUSE_AVX_INSTRUCTIONS=1 -DCUDA_HOST_COMPILER=/usr/bin/gcc-6
$ cmake --build .
$ cd ..
$ sudo python3 setup.py install --set DLIB_USE_CUDA=1 --set USE_AVX_INSTRUCTIONS=1 --set CUDA_HOST_COMPILER=/usr/bin/gcc-6
```
