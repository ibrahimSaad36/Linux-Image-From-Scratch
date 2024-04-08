# Linux-Image-From-Scratch
## Before we start
* The steps of creating a linux image from scratch are: configuring and building the cross-compiler, configuring and 
building the bootloader and then configuring and building the image itself.
* You will find in this repo the sequence and the required commands for doing each step mentioned above, and also I 
will attach my output, it may be a reference to you.
* I was building and configuring each component to work with Q-emu (the emulator that can emulate your physical  machine if you don't have actual hardware) but you can follow the same steps but in configuration, you can choose
your desired hardware and it's very easy.

## We have to download some packages
* First of all, we need to download the following packages and libraries which will be needed later when building our
cross-compiler and u-boot (Don't worry about such things, it will be covered later)

      sudo apt-get update

      sudo apt-get upgrade
  
      sudo apt-get install -y gcc g++ gperf bison flex texinfo help2man make libncurses5-dev 
      python3-dev autoconf automake libtool libtool-bin gawk wget bzip2 xz-utils unzip patch 
      libstdc++6 rsync libssl-dev

**Very Important note:** I was working on this version of Ubuntu (Ubuntu 22.04.2 LTS) you may encounter problems with
the versions of libraries if you are working on previous versions of Ubuntu, for example I was working on Ubuntu 20.04.6 
and I found a problem with the version of libncurses when building the cross-compiler but when I upgraded to 22.04 the
problem was solved.

* We need to clone the tool which will be used to build our cross-compiler (crosstool-ng), run the following command:
    
      git clone https://github.com/crosstool-ng/crosstool-ng.git
      
* In case you're working with hardware, you will need to install arm-gcc compiler

      sudo apt-get install gcc-arm-linux-gnueabi
      
* We will need also to clone the busybox, it will be used later

      git clone git://busybox.net/busybox.git --branch=1_33_0 --depth=1
      
* And of course we need the Linux kernel, after cloning checkout to the stable version v5.19.6

      git clone git://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git
      cd linux/
      git checkout v5.19.6

* Also, clone bootloader (u-boot)
      
      git clone https://github.com/u-boot/u-boot.git
      cd u-boot/
      git checkout v2022.07
      
* Install Q-emu, it will be used as an alternative to hardware

      sudo apt-get install qemu-system
