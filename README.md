# Nvidia-GPU-Install-and-Setup

- [ 1 ](https://qiita.com/shouta-dev/items/428af46b8a61622e25b2)[TitanX Stepup and Issue]
- [ 2 ](http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/) [CUDA Version]



## Step1
### if GPU card be installed on Workstation: 

$ lspci | grep -i NVIDIA <br/>

 if termainal show : VGA compatible controller: NVIDIA Corporation Device 1b00 (rev a1) <br/>

$ sudo update-pciids <br/>

 then you can see : VGA compatible controller: NVIDIA Corporation GP102 [TITAN X] (rev a1) <br/>
 

## Step2
### install CUDA as following:
- [CUDA Install Reference](https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1604&target_type=deblocal)
$ CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.44-1_amd64.deb

$ wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG}

$ sudo dpkg -i /tmp/${CUDA_REPO_PKG} 

$ rm -f /tmp/${CUDA_REPO_PKG}

$ sudo apt-get update

$ sudo apt-get install cuda

$ nano ~/.bashrc
 export CUDA_HOME=/usr/local/cuda-8.0
 export LD_LIBRARY_PATH=${CUDA_HOME}/lib64:$LD_LIBRARY_PATH
 export PATH=${CUDA_HOME}/bin:${PATH}

add in the end, then enter "ctrl+x" to save

$ source ~/.bashrc 

### if key "$ nvidia-smi" show no driver:
$ sudo apt-get install cuda-drivers

$ sudo reboot



