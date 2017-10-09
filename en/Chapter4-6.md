# 4.6 Test USB Host

Connect the USB flash disk to USB HOST(J6) interface, will output detection device information. At the same time, use this storage device to mount the Linux system under its read and write.

```
# usb 1-2: USB disconnect, device number 6
usb 1-2: new high-speed USB device number 7 using atmel-ehci
usb 1-2: New USB device found, idVendor=0bda, idProduct=0316
usb 1-2: New USB device strings: Mfr=1, Product=2, 
SerialNumber=3
usb 1-2: Product: USB3.0-CRW
usb 1-2: Manufacturer: Generic
usb 1-2: SerialNumber: 20120501030900000
usb-storage 1-2:1.0: USB Mass Storage device detected
scsi host5: usb-storage 1-2:1.0
scsi 5:0:0:0: Direct-Access     Generic- SD/MMC           
1.00 PQ: 0 ANSI: 4
sd 5:0:0:0: [sda] 31116288 512-byte logical blocks: (15.9 GB/
14.8 GiB)
sd 5:0:0:0: [sda] Write Protect is off
sd 5:0:0:0: [sda] Write cache: disabled, read cache: enabled, 
doesn't support DPO or FUA
 sda: sda1 sda2
 sd 5:0:0:0: [sda] Attached SCSI removable disk

# mount /dev/sda1 /mnt/
# echo "hello" > /mnt/hello.txt
# cat /mnt/hello.txt
hello
```
