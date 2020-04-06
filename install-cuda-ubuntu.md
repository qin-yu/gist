# How do I Install CUDA on Ubuntu 18.04?

- [How do I Install CUDA on Ubuntu 18.04?](#how-do-i-install-cuda-on-ubuntu-1804)
  - [(DON'T) Add `apt` repo and install CUDA Toolkit (BAD solution)](#dont-add-apt-repo-and-install-cuda-toolkit-bad-solution)
  - [Download and install from official website](#download-and-install-from-official-website)
  - [Problem: what if I want both 10.1 and 10.0?](#problem-what-if-i-want-both-101-and-100)
  - [Reference:](#reference)

## (DON'T) Add `apt` repo and install CUDA Toolkit (BAD solution)
```bash
# 1. do:
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt update
sudo ubuntu-drivers autoinstall
# 2. reboot;
# 3. do:
sudo apt install nvidia-cuda-toolkit gcc-6
nvcc --version
```
However, this gives CUDA 9.1 which doesn't even have a corresponding CuDNN.

## Download and install from official website
So you have to go to the [official CUDA website](https://developer.nvidia.com/cuda-downloads) and download e.g. a .deb file.
Install CUDA 10.1:
```bash
sudo dpkg -i cuda-repo-ubuntu1804_10.1.105-1_amd64.deb
sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub
sudo apt-get update
sudo apt-get install cuda
```
Now everything broke: `apt` cannot `fix` itself.

`sudo apt --fix-broken install` will not work, but:
```bash
sudo apt-get -o Dpkg::Options::="--force-overwrite" install --fix-broken
```
then `apt remove` everything including the old and new CUDA.
then reboot and reinstall CUDA 10.1

## Problem: what if I want both 10.1 and 10.0?
Just get another network .deb file from official website and in the final step:
```bash
sudo apt-get install cuda-10-0
```

## Reference:
- [How do I Install CUDA on Ubuntu 18.04?](https://askubuntu.com/questions/1028830/how-do-i-install-cuda-on-ubuntu-18-04)
- [Failed installation of package breaks apt-get](https://askubuntu.com/questions/1044817/failed-installation-of-package-breaks-apt-get)
