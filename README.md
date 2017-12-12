# Nvidia-GPU-Install-and-Setup

- [ 1 ](https://qiita.com/shouta-dev/items/428af46b8a61622e25b2)[TitanX Stepup and Issue]
- [ 2 ](http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/) [CUDA Version]



## Step1
### if GPU card be installed on Workstation: 
```C++
$ lspci | grep -i NVIDIA <br/>
```
 if termainal show : VGA compatible controller: NVIDIA Corporation Device 1b00 (rev a1) <br/>
```C++
$ sudo update-pciids <br/>
```
 then you can see : VGA compatible controller: NVIDIA Corporation GP102 [TITAN X] (rev a1) <br/>
 

## Step2
### install CUDA as following:
- [CUDA Install Reference](https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1604&target_type=deblocal) <br/>
```C++
$ CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.44-1_amd64.deb

$ wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG}

$ sudo dpkg -i /tmp/${CUDA_REPO_PKG} 

$ sudo apt-get update

$ sudo apt-get install cuda

$ nano ~/.bashrc
 export CUDA_HOME=/usr/local/cuda-8.0 <br/>
 export LD_LIBRARY_PATH=${CUDA_HOME}/lib64:$LD_LIBRARY_PATH <br/>
 export PATH=${CUDA_HOME}/bin:${PATH} <br/>
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



