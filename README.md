# Tensorflow GPU install on ubuntu 18.04(2020/7/1)
### Step 0: Uninstall any Nvidia drivers before
```
sudo apt-get purge nvidia*
sudo apt-get autoremove
sudo apt-get autoclean
sudo rm -rf /usr/local/cuda*

```
### Step 1:Nvidia driver install
