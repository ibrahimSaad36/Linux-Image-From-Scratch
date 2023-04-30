## What is a bootloader?

Bootloader is an application used to flash another code to the flash memory through the flash driver using multiple ways (using 
UART, SPI, CAN, Ethernet, or even USB) which enables you to run multiple applications on your target, for example we may have stm32 
target has an application in the flash memory and we can flash another application in a specific address using a bootloader and then
you can select which one to run easily.

Another example to illustrate the idea is Arduino which has its own pre-implemented bootloader which enables you to write a new 
application using Arduino IDE and then upload this code to the board through USB, and the bootloader takes this new code and replace
the old one and we be able to run this new code easily.

## Why we need a bootloader?

We use bootloaders for two reasons, the first one is for secure booting in which we ensure that every time the device will boot
from a valid address, and the second one is for secure flashing to ensure the integrity of the code to be flashed and apply
security checks to identify the source of this code and then the bootloader will decide whether to flash this code or not.

For example, in a Linux-based system, the bootloader enables us to boot to an existing kernel and then it takes this kernel and 
flash it to RAM so that it can be executed there.

## Booting sequence:

Every device has its own booting sequence and we gonna talk in the following section about some devices:

* **x86 devices**: The first thing in the system that will run is the boot ROM (this chip is programmed by the vendor and it do
  some hardware initialization and checks) then the boot ROM gives the control to the BIOS (Basic Input/Output System, it checks
  system integrity and all connected hardware such as RAM slots are not faulty, also it checks for bootloader in CD-ROM or a
  hard drive depending on the boot option menu) and then the BIOS gives the control to the MBR (Master Boot Record, it recognize 
  the partitions in the systems and loads the bootloader for installed operating system forexample the grub and loads it into
  RAM) then the MBR gives the control to the bootloader of the installed operating system (windows boot loader or grub in case 
  of linux, if you have a dual-boot of linux alongside windows you will see the grub menu which enables you to choose to boot
  to linux or windows) and then the bootloader will load the kernel into RAM and start executing the kernel, then you have the
  system up and running (in case of linux, the bootloader loads the kernel and the device tree binary ot dtb into the RAM and
  then the kernel first load the dtb file and intialize the memory, mount the file ystem and then run the init process).
