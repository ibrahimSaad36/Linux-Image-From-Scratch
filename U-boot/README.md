## What is a bootloader?

Bootloader is an application used to flash another code to the flash memory through the flash driver using multiple ways (using 
UART, SPI, CAN, Ethernet or even USB) which enables you to run multiple applications on your target, for example we may have stm32 
target has an application in the flash memory and we can flash another application in specific address using a bootloader and then
you can select which one to run easily.

Another esample to illustrate the idea os Arduino which has its own preimplemented bootloader which enables you to write a new 
application using Arduino IDE and then upload this code to the broad through USB, and the bootloader takes this new code and replace
the old one and we be able to run this new code easily.

## Why we need a bootloader?

We use bootloaders for two reasons, the first one is for secure booting in which we ensure that every time the device will boot
from a valid address, and the second onw is for secure flashing to ensure the integrity of the code to be flashed and apply
security checks to identify the source of this code and then the bootloader will decide to flash this code or not.

For example, in linux-based system the bootloader enables us to boot to an existing kernel and then it takes this kernel and 
flash it to RAM so that it can be executed there.

## Booting sequence:

Every device has its own booting sequence and we gonna talk in the following section about some devices:

* **x86 devices**
