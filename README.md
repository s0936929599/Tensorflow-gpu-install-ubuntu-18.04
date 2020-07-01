# Tensorflow GPU install on ubuntu 18.04(2020/7/1)
### Step 0: Uninstall any Nvidia files before
```

sudo apt-get purge nvidia*
sudo apt-get autoremove
sudo apt-get autoclean
sudo rm -rf /usr/local/cuda*

```
### Step 1:Nvidia driver install
```
sudo add-apt-repository -y ppa:graphics-drivers/ppa
sudo apt-get update
sudo apt-get install nvidia-driver-440
sudo reboot

```
**Check install successfully or not**
```
nvidia-smi

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
### Step 2:Install CUDA 10.2 [Here](https://developer.nvidia.com/cuda-10.2-download-archive?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1804&target_type=deblocal)
