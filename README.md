# Nvidia-GPU-Install-and-Setup

- [the lasterst install reference:Ubuntu1604+CUDA9.0+Cudnn7.5+Caffe+digits](http://blog.csdn.net/linyu2016/article/details/78903243)
- [ 1 ](https://qiita.com/shouta-dev/items/428af46b8a61622e25b2)[TitanX Stepup and Issue]
- [ 2 ](http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/) [CUDA Version]
- [CUDA-9.0](https://developer.nvidia.com/cuda-90-download-archive?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1604&target_type=deblocal)
<br/>

### brfore startup GPU you need to install Opencv2.4.13

## Step1
### if GPU card be installed on Workstation: 
```C++
$ lspci | grep -i NVIDIA
```
 if termainal show : VGA compatible controller: NVIDIA Corporation Device 1b00 (rev a1) <br/>
 you can try sa following: <br/>
```C++
$ sudo update-pciids
```
 then you can see : VGA compatible controller: NVIDIA Corporation GP102 [TITAN X] (rev a1) <br/>
 <br/>

## Step2
### install CUDA as following:
- [CUDA Toolkit Download](https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1604&target_type=deblocal) <br/>
- [CUDA Install Guide Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/n-series-driver-setup)

**Using "cuda8.0" version for example:** 
```C++
$ CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

$ wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG}

$ sudo dpkg -i /tmp/${CUDA_REPO_PKG} 

$ sudo apt-get update

$ sudo apt-get install cuda-8-0

$ nano ~/.bashrc
 export CUDA_HOME=/usr/local/cuda-8.0
 export LD_LIBRARY_PATH=${CUDA_HOME}/lib64:$LD_LIBRARY_PATH
 export PATH=${CUDA_HOME}/bin:${PATH}
```
add in the end, then enter "ctrl+x" to save <br/>
```C++
$ source ~/.bashrc

$ sudo reboot
```
<br/>

than update cuda driver:
```C++
$ sudo ubuntu-drivers autoinstall
```
<br/>

then you can try key **"nvcc -V"** can see: <br/>

nvcc: NVIDIA (R) Cuda compiler driver <br/>
Copyright (c) 2005-2016 NVIDIA Corporation <br/>
Built on Tue_Jan_10_13:22:03_CST_2017 <br/>
Cuda compilation tools, release 8.0, V8.0.61 <br/>

```C++
$ rm -f /tmp/${CUDA_REPO_PKG}
```
### if key "$ nvidia-smi" show no driver:
```C++
$ sudo apt-get install cuda-drivers

$ sudo reboot
```
then you can try again key **"nvidia-smi"** <br/>


### Run CUDA Sample Code:
```C++
$ cd /usr/local/cuda-8.0/samples/1_Utilities/deviceQuery
$ sudo make
$./deviceQuery
```
then you can see everything basic GPU information about your GPU card <br/>
<br/>

---

### If you meet login loop problem, you can key 'Ctrl + Alt + F1' to terminal mode than:
```C++
$ nvidia-smi
```
<br/>

**if show no drivers, then you can try as follow cammand:**
```C++
$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo ubuntu-drivers autoinstall
```
<br/>

---

## Step3
### Install cuDNN 5.1:
- [cuDNN Download ](https://developer.nvidia.com/rdp/cudnn-download)

According your CUDA Version then choose **cuDNN v5.1 Library for Linux** to download
```C++
$ cd 下載

$ tar xvzf cudnn-8.0-linux-x64-v5.1.tgz
$ tar xvzf cudnn-8.0-linux-x64-v6.0.tgz

$ sudo cp -P cuda/include/cudnn.h /usr/local/cuda-8.0/include 

$ sudo cp -P cuda/lib64/libcudnn* /usr/local/cuda-8.0/lib64

$ sudo chmod a+r /usr/local/cuda-8.0/include/cudnn.h /usr/local/cuda-8.0/lib64/libcudnn*  
```
<br/>

**ignore temporatory** <br/>
### create soft link:
```C++
////=========cudnn5.1=========
$ sudo ln -s libcudnn.so.5.1.10 libcudnn.so.5

$ sudo ln -s libcudnn.so.5 libcudnn.so

////=========cudnn7.0=========

$ sudo ln -s libcudnn.so.7.0.5 libcudnn.so.7

$ sudo ln -s libcudnn.so.7 libcudnn.so
```
**ignore temporatory** <br/>
<br/>

## Step4
### install caffe:
- [Caffe](http://caffe.berkeleyvision.org/install_apt.html)
- [BVLC/Caffe Installation Guide](https://github.com/BVLC/caffe/wiki/Ubuntu-16.04-or-15.10-Installation-Guide)
```C++

$ git clone https://github.com/BVLC/caffe.git

$ sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler

$ sudo apt-get install --no-install-recommends libboost-all-dev

$ sudo apt-get install libatlas-base-dev 

$ sudo apt-get install libopenblas-dev
 
$ sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev

$ sudo apt-get install -y python-pip
//=== python2.7 ===
$ sudo apt-get install -y python-dev

$ sudo apt-get install -y python-numpy python-scipy
//=== python3.5 ===
$ sudo apt-get install -y python3-dev

$ sudo apt-get install -y python3-numpy python3-scipy
//=================
$ cd caffe/python/

$ for req in $(cat requirements.txt); do sudo -H pip install $req --upgrade; done

$ sudo apt-get update

$ cp Makefile.config.example Makefile.config

Open Makefile.config to change:

# USE_CUDNN := 1   ---->   USE_CUDNN := 1
# CUDA_DIR := /usr/local/cuda   ---->   CUDA_DIR := /usr/local/cuda-8.0
# INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include /usr/include/hdf5/serial
# LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/x86_64-linux-gnu /usr/lib/x86_64-linux-gnu/hdf5/serial
# PYTHON_INCLUDE := /usr/include/python2.7 /usr/lib/python2.7/dist-packages/numpy/core/include  
```
<br/>

---

### The build process will fail in Ubuntu 16.04. Edit the Makefile with an editor such as
```C++
$ nano ./Makefile
```
**and replace this line:**
```C++
 NVCCFLAGS += -ccbin=$(CXX) -Xcompiler -fPIC $(COMMON_FLAGS)
```
**with the following line:*
```C++
NVCCFLAGS += -D_FORCE_INLINES -ccbin=$(CXX) -Xcompiler -fPIC $(COMMON_FLAGS)
```
**Also, open the file CMakeLists.txt and add the following line:**
```C++
# ---[ Includes
set(${CMAKE_CXX_FLAGS} "-D_FORCE_INLINES ${CMAKE_CXX_FLAGS}")
```
**(See the discussion at: https://github.com/BVLC/caffe/issues/4046)**
<br/>

### add opencv dependency requires in caffe "CMakeLists.txt" file as follows:

```C++

set( OpenCV_DIR "/home/ubuntu/opencv-2.4.13/release/" ) ###
find_package(OpenCV REQUIRED) ###

```
<br/>

### create caffe thirdparty lib symbolic link: 
```C++
$ cd /usr/lib/x86_64-linux-gnu

$ sudo ln -s libhdf5_serial.so.10.1.0 libhdf5.so

$ sudo ln -s libhdf5_serial.so.10.1.0 libhdf5_hl.so
```
if you need to delete symbolic link:
```C++
$ rm -rf /usr/lib/x86_64-linux-gnu/libhdf5_hl.so /usr/lib/x86_64-linux-gnu/libhdf5_serial_hl.so.10.1.0

$ rm -rf /usr/lib/x86_64-linux-gnu/libhdf5_serial.so.10.1.0 /usr/lib/x86_64-linux-gnu/libhdf5.so
```
<br/>

### make caffe:
```C++
$ cd caffe

$ mkdir build

$ cmake ..

$ make all

$ make runtest
```
<br/>

### 配置pycaffe:

```C++
$ sudo apt-get install python-numpy python-scipy python-matplotlib python-sklearn python-skimage python-h5py python-protobuf python-leveldb python-networkx python-nose python-pandas python-gflags cython ipython

$ sudo apt-get install protobuf-c-compiler protobuf-compiler

$ cd ~/caffe/build

$ make pycaffe

```
<br/>


**ignore tmp**
```C++
$ sudo gedit /etc/profile # 末尾添加： export PYTHONPATH = caffe目录下的python地址:$PYTHONPATH，用完整路径，不要用~

for example:
export PYTHONPATH=/home/ubuntu/caffe/python/:$PYTHONPATH

$ source /etc/profile # 使之生效
```
**ignore tmp**<br/>
<br/>
<br/>

```C++
$ nano ~/.bashrc
export PYTHONPATH=/home/ubuntu/caffe/build/python/:$PYTHONPATH

$ source ~/.bashrc

$ cd caffe

$ make distribute

```
<br/>

### test caffe in python
```C++
$ python
>>>import caffe
```
**If show:**
```C++
>>> import caffe
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ImportError: No module named caffe
```
**then**
```C++
$ nano ~/.bashrc
export PYTHONPATH=/home/ubuntu/caffe/distribute/python/:$PYTHONPATH

$ source ~/.bashrc
```
<br/>

#### 使用MNIST数据集进行测试:
```C++
$ cd caffe
$ sh data/mnist/get_mnist.sh
$ sh examples/mnist/create_mnist.sh
$ sh examples/mnist/train_lenet.sh
```
<br/>

## Step5
### Install Digits:

1. - [BuildCaffe.md](https://github.com/NVIDIA/DIGITS/blob/master/docs/BuildCaffe.md)

2. - [BuildDigits](https://github.com/NVIDIA/DIGITS/blob/master/docs/BuildDigits.md)

```C++
$ DIGITS_ROOT=~/digits

$ git clone https://github.com/NVIDIA/DIGITS.git $DIGITS_ROOT

$ sudo pip install -r $DIGITS_ROOT/requirements.txt

$ sudo pip install -e $DIGITS_ROOT

$cd digits

$./digits-devserver

Starts a server at http://localhost:5000/

```
<br/>

If show **A valid Caffe installation was not found on your system. Use the envvar CAFFE_ROOT to indicate a valid installation.**

### These instructions are for bash
```C++
$ echo $SHELL
/bin/bash
```

### Check the current value of your envvar
```C++
$ echo $CAFFE_ROOT
```

### Add the envvar to ~/.profile so it will load automatically when you login
```C++
$ echo "export CAFFE_ROOT=/home/username/caffe/" >> ~/.profile
```

### Load the new configuration
```C++
$ source ~/.profile
```

### Check the new envvar value
```C++
$ echo $CAFFE_ROOT
/home/username/caffe/
```
