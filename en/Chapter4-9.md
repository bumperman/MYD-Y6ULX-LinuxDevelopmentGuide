# 4.9 Test CAN Bus

Attention: This example needs install the MYB-6ULX on MYS-6ULX-IOT or MYS-6ULX-IND.And uses dtb file to boot Linux that supoorts MYB-6ULX board.

This example demonstrates the use of the Linux API, which uses the CAN bus interface on the development board to send and receive data. Copy can_send and can_receive to the development board. Perform the following steps

MYD-JA5D2X board has one CAN bus interface(J20), which can communicate with other CAN node device.

## Hareware connect
MYB-6ULX board has an CAN bus interface(J11).You need connect the H, L data signal to another CAN device or USB to CAN converter.

## Software

Configure the CAN0 bitrate is 50kbps and enable it.

Linux has two commands to configure CAN device, canconfig and ip. The MYS-6ULX use ip as default.
canconfig command usage:
```
canconfig can0 bitrate 50000 ctrlmode triple-sampling on
canconfig can0 start
```
ip command usage:
```
ip link set can0 type can bitrate 50000 triple-sampling on
ifconfig can0 up
```

Next, we use cansend/candump command and can_send/can_receive program to test CAN device.The cansend/candump is buildin system rootfs.The can_send/can_receive is our example program.

- MYB-6ULX as sender

Use cansend send data to CAN bus:
```
cansend can0 100#01.02.03.04.05.06.07.08
```

can_send program will sending loop, unitl you use "ctrl + c" to stop it.
```
./can_send -d can0 -i 100 0x11 0x22 0x33 0x44 0x55 0x66 0x77 0x88
```

- MYB-6ULX as receiver

Use candump receive data from CAN bus:
```
candump can0
can0  100   [8]  01 02 03 04 05 06 07 08
```
Use can_receive program receive data from CAN bus:
```
can0  0x100  [8]  0x11 0x22 0x33 0x44 0x55 0x66 0x77 0x88 
can0  0x100  [8]  0x11 0x22 0x33 0x44 0x55 0x66 0x77 0x88 
can0  0x100  [8]  0x11 0x22 0x33 0x44 0x55 0x66 0x77 0x88 
can0  0x100  [8]  0x11 0x22 0x33 0x44 0x55 0x66 0x77 0x88
...