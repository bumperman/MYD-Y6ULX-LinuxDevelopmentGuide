# 3.1 BootLoader

MYD-JA5D2X has two levels bootLoader, AT91Bootstrap and U-Boot.

After the system is powered up, the CPU automatically copies the AT91Bootstrap binary program from the external storage device to the internal SRAM and starts execution. Its main role is to initialize the CPU, DDR RAM and U-Boot storage device, and the U-Boot binary program copied to memory, and then jump to U-Boot program entry to start it.

* First level bootloader AT91Bootstrap, used for init CPU, RAM and necessary peripherial device, it will load and boot U-Boot.
* Second level bootloader U-Boot used for load, boot and update kernel image. It also supports multiple boot type and interactive CLI interface.
