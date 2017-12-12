# Nvidia-GPU-Install-and-Setup

- [ 1 ](https://qiita.com/shouta-dev/items/428af46b8a61622e25b2)[TitanX Stepup and Issue]
- [ 2 ](http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/) [CUDA Version]



## Step1
### if GPU card be installed on Workstation 

$ lspci | grep -i NVIDIA <br/>

 if termainal show : VGA compatible controller: NVIDIA Corporation Device 1b00 (rev a1) <br/>

$ sudo update-pciids <br/>

 than you can see : VGA compatible controller: NVIDIA Corporation GP102 [TITAN X] (rev a1) <br/>
 

## Step2

