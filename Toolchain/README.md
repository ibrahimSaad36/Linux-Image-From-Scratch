# Toolchain and the cross-compiler

You will find a cross-compiler after configuration and build for arm-cortexa9_neon-linux-gnueabihf in this 
[LINK](https://drive.google.com/file/d/1e9vzTqpFacTJGWLtACskvlhF0VMo35s8/view?usp=share_link)

### Why we need a compiler?

Because we have the source code (C code) of the bootloader and the kernel itself, we don't have the binaries but we need the hex files
or the binaries to run on the target.

The reason why we have only the source code is that this source code can be configured every time you change the hardware and
build it again with a different compiler to get binaries that can run on your new hardware.

### Why we need a cross-compiler?

Because the target architecture differs from the architecture of the host machine (the host machine is the machine you're writing the code on it and compile this code to run it on a different machine) which means different ISA, different considerations
such as if this target supports hardware FPU or the compiler will handle all floating point computations on its own, also if the target
is little endian or big Indian so, we need a compiler that can understand the target's ISA and the architecture.

### Difference between toochain and the compiler:

The compiler is a component of the toolchain, but the toolchain contains other components which are used in the build process such as:

* Binutils: which contains some tools such as: assembler, linker, ar (which generates archives for the libraries), readelf, objdump
  nm, size, and other tools.
* C library and other programs to communicate with the kernel header (C library examples: glibc, musl, embedded glibc, uclibc), 
  for additional information [check this link](https://elinux.org/Toolchains)
* Debugger which enables you to debug code and find the bugs, also you can see the assembly code, insert breakpoints, and so on.
  (example for the debugger, the gdb which comes with GCC compiler)

### Steps to build your cross-compiler:

We have already cloned the crosstool-ng tool which is used to configure and build the compiler among many architectures supported 
by crosstool-ng and here you are the steps to configure and build the compiler:

**Note:** I assumed that you have cloned the crosstool-ng into your home directory but in case you have a different working path
you should handle all relative paths.

1- Go inside crosstool-ng directory and setup the environment

      cd crosstool-ng/
      
      # Setup the environment
      
      ./bootstrap 

2- Check all dependencies are ok

      ./configure --enable-local
      
3- Generate Makefile for crosstool-ng

      make
      
4- Time for configuration, we will use arm-cortexa9_neon-linux-gnueabihf but you can choose whatever you want

      # See all avilable architectures
      ./ct-ng list-samples
      
      # You can search for a specific architecture by using grep
      ./ct-ng list-samples | grep <architecture>
      
5- Configure the architecture

      ./ct-ng <architecture>
      
      # In our case to use Q-emu 
      
      ./ct-ng arm-cortexa9_neon-linux-gnueabihf
      
6- Choose the configurations you want

      ./ct-ng menuconfig

It will open a GUI menu for you to choose the configuration of the compiler, for example you can specify the C library you want,
choose if your compiler supports C++ or not, configure debugger and binutils.

The menu will appear like this, feel free to explore all the configurations in this window and you can search for something by 
writing / and then a search window will be opened, type anything you want and it will give you where you can find it

   ![8BH8R](https://user-images.githubusercontent.com/118214245/233126057-8d4f9288-0e0b-4b80-8a70-0b018cb83591.jpg)

7- Time to build, make sure you finished all the configurations before building and make sure that your laptop's screen won't
be turned off, and the laptop is plugged into the power as the process is long (for me it took about 222 minutes to finish)

      ./ct-ng build
      
 Wait until build process is completed and note that warnings are ok, hope to you a smooth build without errors :)
 
 After build is finished check the output (you will find all output directories and binaries in directory named x-tools in
 your home directory), you will find some directories such as:
 
 * bin directory which include the vinaries such as yourCompiler-gcc, yourCompiler-ld ans son on.
 * sysroot directory (x-tools\arm-cortexa9_neon-linux-gnueabihf\arm-cortexa9_neon-linux-gnueabihf\sysroot), it's important
   the directory which includes libraries and headers needed to compile a program for the target
 
 Now you're ready to go into the next step ENJOY :)
      
