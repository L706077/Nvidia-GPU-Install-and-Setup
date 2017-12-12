# Nvidia-GPU-Install-and-Setup

- [ 1 ](https://qiita.com/shouta-dev/items/428af46b8a61622e25b2)[TitanX Stepup and Issue]
- [ 2 ](http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/) [CUDA Version]



## Step1
### if GPU card be installed on Workstation: 
```C++
$ lspci | grep -i NVIDIA
```
 if termainal show : VGA compatible controller: NVIDIA Corporation Device 1b00 (rev a1) <br/>
```C++
$ sudo update-pciids
```
 then you can see : VGA compatible controller: NVIDIA Corporation GP102 [TITAN X] (rev a1) <br/>
 

## Step2
### install CUDA as following:
- [CUDA Toolkit Download](https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1604&target_type=deblocal) <br/>
```C++
$ CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.44-1_amd64.deb

$ wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG}

$ sudo dpkg -i /tmp/${CUDA_REPO_PKG} 

$ sudo apt-get update

$ sudo apt-get install cuda

$ nano ~/.bashrc
 export CUDA_HOME=/usr/local/cuda-8.0
 export LD_LIBRARY_PATH=${CUDA_HOME}/lib64:$LD_LIBRARY_PATH
 export PATH=${CUDA_HOME}/bin:${PATH}
```
add in the end, then enter "ctrl+x" to save <br/>
```C++
$ source ~/.bashrc 
```
then you can try key **"nvcc -V"** can see: <br/>

nvcc: NVIDIA (R) Cuda compiler driver <br/>
Copyright (c) 2005-2017 NVIDIA Corporation <br/>
Built on Fri_Nov__3_21:07:56_CDT_2017 <br/>
Cuda compilation tools, release 9.1, V9.1.85 <br/>
```C++
$ rm -f /tmp/${CUDA_REPO_PKG}
```
### if key "$ nvidia-smi" show no driver:
```C++
$ sudo apt-get install cuda-drivers

$ sudo reboot
```
then you can try again key **"nvidia-smi"** <br/>

## Step3
### Run CUDA Sample Code:
```C++
$ cd /usr/local/cuda-9.1/samples/1_Utilities/deviceQuery
$ sudo make
$./deviceQuery
```
then you can see everything basic GPU information about your GPU card <br/>


## Step4
### Install cuDNN 7.0
- [cuDNN Download ](https://developer.nvidia.com/rdp/cudnn-download)

According your CUDA Version then choose ** cuDNN v7.0.5 Library for Linux ** to download
```C++
$ cd 下載

$ tar xvzf cudnn-9.1-linux-x64-v7.tgz

$ sudo cp -P cuda/include/cudnn.h /usr/local/cuda-9.1/include 

$ sudo cp -P cuda/lib64/libcudnn* /usr/local/cuda-9.1/lib64

$ sudo chmod a+r /usr/local/cuda-9.1/include/cudnn.h /usr/local/cuda-9.1/lib64/libcudnn*  
```

**ignore temporatory** <br/>
### create soft link:
```C++
$ sudo ln -s libcudnn.so.7.0.5 libcudnn.so.7

$ sudo ln -s libcudnn.so.7 libcudnn.so
```
**ignore temporatory** <br/>


## Step5
```C++

$ git clone https://github.com/BVLC/caffe.git

$ sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler

$ sudo apt-get install --no-install-recommends libboost-all-dev
 
$ sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev


```
