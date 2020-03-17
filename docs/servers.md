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

| IP           | Domain            | GPUs                    | CUDA version |
|--------------|-------------------|-------------------------|--------------|
| 172.16.33.17 | inanna.cs.uml.edu | 3x GTX 1080             | 10.2         |
| 172.16.33.13 | enki.cs.uml.edu   | 2x Titan X              | 9.1          |
| 172.16.33.15 | shala.cs.uml.edu  | 3x GTX 1080             | 10.1         |
| 172.16.33.14 | ishkur.cs.uml.edu | 2x GTX 1080, 1x Titan X | 10.1         |
| 172.16.33.9  | marduk.cs.uml.edu | 3x Tesla K40 (outdated) | ??           |

CPU-only:

* dumuzi.cs.uml.edu

If you have problems connecting to a server or wish to create an account, please contact the corresponding administrator.
If you don’t currently have an account, you can use the teaching lab’s workstations in DAN417 (each one of them has a GPU).

## Installing drivers and CUDA

Follow [this guide](https://gist.github.com/wangruohui/df039f0dc434d6486f5d4d098aa52d07)

Recommendations: 
  * Use `Latest Long Lived Branch` for drivers
  * Do everything in tmux session in case ssh connection is interrupted (it will!)
  * Call `sudo ./cuda_10.2.89_440.33.01_linux.run` instead of `./cuda_10.2.89_440.33.01_linux.run`
  * After installing cuda you may see a warning `Incomplete installation! This installation did not install the CUDA Driver.` - don't worry, just ignore it (you already have the driver)
  * Remember to install [cuDNN](https://developer.nvidia.com/cudnn)! Select "cuDNN Library for Linux" instead of "cuDNN Runtime Library for Ubuntu18.04 (Deb)" because you don't want to suffer deleteing .deb packages when reinstalling the CUDA next time. You cannot use `wget` to download cuDNN (because NVIDIA sucks) so download it to your computer and `scp` to the server.
  * Untar cuDNN as `sudo` to create symlinks

Possible issues:
  * "Existing package manager installation of the driver found" - the problem is that somebody installed CUDA via package manager (you sick bastard!). You need to find what exactly is installed and delete is using `sudo apt-get purge <PACKAGE_NAME>` and to execute `sudo apt autoremove` after that. You can also try to do this (but the result and safety of these commands are not guaranteeed):

```bash
sudo apt-get purge cuda
sudo apt-get purge nvidia-cuda-toolkit
sudo apt-get purge "cuda*"
sudo apt autoremove
```

  * "Installation failed. See log at /tmp/cuda-installer.log for details" - see the log first. If this is driver error, just remove [x] from driver installation when installing cuda (we installed the driver at the previous step, remember?)

## Installing Apex

[Nvidia Apex](https://github.com/NVIDIA/apex) is a library that allows you to speed up training / reduce memory requirements in just a few lines of code (or no code at all!). It is used in many externali libraries (like fairSeq and Megatron) and just makes things better. Use it.

Follow installation instructions in the official README.md

Possible issues:
  * If your CUDA version does not match Apex version completely, installation will fail on purpose ("Cuda extensions are being compiled with a version of Cuda that does not match the version used to compile Pytorch binaries"). To get around this you can comment out this check in setup.py file and hope for the best.

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
