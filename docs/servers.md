> How to create/restore an account, who has sudo, soft- and hardware setups, ...
---

# Compute Resources

## Servers

We currently have 5 servers with GPUs installed and 1 server with a lot of memory but no GPU.
All servers run Ubuntu, so you should be comfortable constantly typing commands in a terminal.
A quick reference of the most used bash commands can be found here.
To connect to a server, you need to be within the UML network: this can be done using a PulseSecure VPN client,
or by first logging into “cs” server using your cs credentials and then jumping to one of our servers. 
For establishing an ssh connection, you can either use IPs or server names as follows:

GPU-enabled:
* 172.16.33.17 - inanna.cs.uml.edu - 3x GTX 1080
* 172.16.33.13 - enki.cs.uml.edu - 2x Titan X
* 172.16.33.15 - shala.cs.uml.edu - 3x GTX 1080
* 172.16.33.14 - ishkur.cs.uml.edu - 2x GTX 1080, 1x Titan X
* 172.16.33.9 - marduk.cs.uml.edu - 3x Tesla K40 (outdated)

CPU-only:
* dumuzi.cs.uml.edu

If you have problems connecting to a server or wish to create an account, please contact the corresponding administrator.
If you don’t currently have an account, you can use the teaching lab’s workstations in DAN417 (each one of them has a GPU).

## Installing drivers and CUDA

> This guide ~~may be~~ is outdated. **Think** before doing anything

1. Install the drivers using the graphics-drivers ppa:
    1. Link: https://launchpad.net/~graphics-drivers/+archive/ubuntu/ppa
    1. Add ppa: sudo add-apt-repository ppa:graphics-drivers/ppa
    1. Update apt-get: sudo apt-get update
    1. Install the drivers: apt-get install nvidia-430 (you’d need to replace `430` with the current long-lived release
    1. Reboot the system

1. Install cuda using the run-file installer
    1. Link: https://developer.nvidia.com/cuda-zone

1. `sudo sh cuda_<version>_linux.run`
    1. Do not agree to install the drivers
    1. Do not agree to install OpenCL
    1. Agree to install only the CUDA and, maybe, CUDA samples
    1. Do not forget to run ldconfig after the installation 
    1. Create a file /etc/ld.so.conf.d/cuda.conf
    1. Insert the path to the cuda’s lib dir into this file: /usr/local/cuda/lib64
    1. Run sudo ldconfig
    1. Add the bin dir to your PATH variable
    1. See here: https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#post-installation-actions
    1. Or, to install it globally, add `PATH=$PATH:/usr/local/cuda/bin` to `/etc/profile` text file (sudo required)

1. Install cuDNN using by copying the files 
    1. [Link](https://developer.nvidia.com/cudnn)
    1. Extract the downloaded archive
    1. Copy the files:
    ```
    cd <path to the content>
    sudo cp -P include/cudnn.h /usr/local/cuda/include/
    sudo cp -P lib64/libcudnn* /usr/local/cuda/lib64/
    sudo chmod a+r /usr/local/cuda/lib64/libcudnn*
    ```
1. Reboot the system
1. Run nvidia-smi to check that GPUs are visible

## User management

In general, all user accounts should have the name following the template <first letter of first name><last name>.
For example, for a user Alexey Romanov, the username would be `aromanov`.

## Useful commands

* View all users: `getent passwd`
* View sudo users: `getent group sudo | cut -d: -f4`
* Delete user from sudo: `sudo deluser USERNAME sudo`
* Add user to sudo: `sudo usermod -aG sudo USERNAME`
* Add user: `sudo adduser USERNAME`
* Add a group: `sudo addgroup GROUPNAME`
* Set primary group: `usermod -g GROUPNAME USERNAME`

## Some of administrator responsibilities

* All servers must run Ubuntu release that is a) supported b) LTS (long-term). Best, if it is the latest LTS.
* CUDA should be updated such that the latest version of PyTorch supports it.

## Other resources

* Digital Ocean Droplets and university infrastructure (if you need to host a servise)
* Multiple GPUs (days of compute): just learn PyTorch Distributed to utilize multiple GPUs
    * [official guide](https://pytorch.org/tutorials/intermediate/dist_tuto.html) (which we do not recommend)
    * [related medium post](https://medium.com/huggingface/training-larger-batches-practical-tips-on-1-gpu-multi-gpu-distributed-setups-ec88c3e51255)
    * [lightning](https://towardsdatascience.com/how-to-refactor-your-pytorch-code-to-get-these-42-benefits-of-pytorch-lighting-6fdd0dc97538) module which makes it very easy to use
    * You can also use PyTorch DataParallel (and it is easier), but it is less efficient
    * **Note:** always test that your multi-GPU setup if actually faster than a single GPU on a small subset of your data
* [TensorFlow Research Cloud](https://www.tensorflow.org/tfrc) (months of compute): TFRC allows to access free TPUs for research purposes, consult with somebody from the lab before applying

## If you need help

You can ask any hardware-related questions in Slack #hardware channel
