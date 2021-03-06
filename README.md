# Tensorflow GPU install on ubuntu 18.04(2020/7/1)

## RTX2060 super + CUDA v10.0 + cuDNN v7.6.5

### Step 0: Uninstall any Nvidia files before
```

sudo apt-get purge nvidia*
sudo apt-get autoremove
sudo apt-get autoclean
sudo rm -rf /usr/local/cuda*

```
### Step 1: Nvidia driver install
```
sudo add-apt-repository -y ppa:graphics-drivers/ppa
sudo apt-get update
sudo apt-get install nvidia-driver-440
sudo reboot

```
**Check the installation successful or not**
```
nvidia-smi
```
Output:
```
Wed Jul  1 16:31:07 2020       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 440.100      Driver Version: 440.100      CUDA Version: 10.2     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce RTX 206...  Off  | 00000000:01:00.0  On |                  N/A |
| 38%   30C    P8     3W / 175W |    525MiB /  7977MiB |      3%      Default |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|    0      2112      G   /usr/lib/xorg/Xorg                            18MiB |
|    0      2316      G   /usr/bin/gnome-shell                          56MiB |
|    0      3380      G   /usr/lib/xorg/Xorg                           136MiB |
|    0      3608      G   /usr/bin/gnome-shell                         124MiB |
|    0      4377      G   ...AAAAAAAAAAAACAAAAAAAAAA= --shared-files    96MiB |
|    0     23015      C   /usr/bin/python3                              87MiB |
+-----------------------------------------------------------------------------+
```
### Step 2: Install CUDA v10.0 [Here](https://developer.nvidia.com/cuda-10.0-download-archive?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1804&target_type=deblocal)

![image](https://github.com/s0936929599/Tensorflow-gpu-install-ubuntu-18.04/blob/master/cuda.png)

**Installation Instructions**
```
sudo dpkg -i cuda-repo-ubuntu1804-10-0-local-10.0.130-410.48_1.0-1_amd64.deb
sudo apt-key add /var/cuda-repo-10-0-local-10.0.130-410.48/7fa2af80.pub
sudo apt-get update
sudo apt-get install cuda-toolkit-10-0

```
### Step 3: Add CUDA to ENV variables(path:~/.bashrc)

**Open .bashrc and add below commands to the bottom**

```
export PATH=/usr/local/cuda-10.0/bin${PATH:+:$PATH}
export LD_LIBRARY_PATH=/usr/local/cuda-10.0/lib64:$LD_LIBRARY_PATH
```

**Compiler .bashrc**
```
source ~/.bashrc
sudo ldconfig

```

**Check ENV variables**
```
nvcc -V

```
Output:
```

nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2018 NVIDIA Corporation
Built on Sat_Aug_25_21:08:01_CDT_2018
Cuda compilation tools, release 10.0, V10.0.130

```
### Step 4: Download cuDNN v7.6.5 [Here](https://developer.nvidia.com/rdp/cudnn-download) and install
```
sudo dpkg -i libcudnn7_7.6.5.32-1+cuda10.0_amd64.deb

```
### Step 5: Install tensorlow-gpu and Keras
  ~~pip3 install tensorflow-gpu~~  -> pip3 install tensorflow-gpu==1.14.0 
  
  ~~pip3 install keras~~  -> pip3 install keras==2.3.1
##### Verify your tensorflow installation in python

```
from tensorflow.python.client import device_lib

print(device_lib.list_local_devices())
```
Output:
```
[name: "/device:CPU:0"
device_type: "CPU"
memory_limit: 268435456
locality {
}
incarnation: 5050412522266903105
, name: "/device:XLA_GPU:0"
device_type: "XLA_GPU"
memory_limit: 17179869184
locality {
}
incarnation: 18125124559370062919
physical_device_desc: "device: XLA_GPU device"
, name: "/device:XLA_CPU:0"
device_type: "XLA_CPU"
memory_limit: 17179869184
locality {
}
incarnation: 14298016103877147071
physical_device_desc: "device: XLA_CPU device"
]

```

### Optional: If encounter cuDNN error add these in front of your code

```
import tensorflow as tf

config = tf.ConfigProto()
config.gpu_options.allow_growth = True
sess = tf.Session(config=config)

```
