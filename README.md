# faceRecognizer with GPU

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
# 7. Check if CUDA suppored again!
```
$ python3
Python 3.8.10 (default, Jun  2 2021, 10:49:15) 
[GCC 9.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import dlib
>>> dlib.DLIB_USE_CUDA
True
```
# 8. Install face_recognition again
```
$ sudo pip3 install face_recognition
```

# 9. Run your video streaming app and check GPU offloading thru nvidia-smi!
```
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 470.57.02    Driver Version: 470.57.02    CUDA Version: 11.4     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  Quadro P1000        On   | 00000000:04:00.0 Off |                  N/A |
| 44%   59C    P0    N/A /  N/A |    393MiB /  4040MiB |     48%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A      1113      G   /usr/lib/xorg/Xorg                  4MiB |
|    0   N/A  N/A      1627      G   /usr/lib/xorg/Xorg                  4MiB |
|    0   N/A  N/A      9151      C   python3                           380MiB |
+-----------------------------------------------------------------------------+
```
