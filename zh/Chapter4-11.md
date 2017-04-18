# 4.11 USB HOST/DEVICE 测试

本例程演示使用开发板的USB MINI(J18)接口可以将指定的文件或设备模拟为Gadget设备。这里把内存作为存储设备提供给HOST设备。

- 开发板上操作:

```
mkfs.vfat /dev/ram1
insmod atmel_usba_udc libcomposite usb_f_mass_storage
insmod g_mass_storage.ko file=/dev/ram1 removable=1 iSerialNumber="1234"
Number of LUNs=8
Mass Storage Function, version: 2009/09/11
LUN: removable file: (no medium)
Number of LUNs=1
LUN: removable file: /dev/ram1
Number of LUNs=1
g_mass_storage gadget: Mass Storage Gadget, version: 2009/09/11
g_mass_storage gadget: g_mass_storage ready
# g_mass_storage gadget: high-speed config #1: Linux File-Backed Storage
```

- PC机上查看到有USB设备接入，SerialNumber为"1234":

```
dmesg | tail -n 20
[516310.646369] usb 1-2.4: new high-speed USB device number 105 using xhci_hcd
[516310.734966] usb 1-2.4: New USB device found, idVendor=0525, idProduct=a4a5
[516310.734970] usb 1-2.4: New USB device strings: Mfr=3, Product=4, SerialNumber=5
[516310.734973] usb 1-2.4: Product: Mass Storage Gadget
[516310.734975] usb 1-2.4: Manufacturer: Linux 4.1.0-linux4sam_5.3+ with atmel_usba_udc
[516310.734977] usb 1-2.4: SerialNumber: 1234
[516310.741963] usb-storage 1-2.4:1.0: USB Mass Storage device detected
[516310.742073] usb-storage 1-2.4:1.0: Quirks match for vid 0525 pid a4a5: 10000
[516310.742091] scsi27 : usb-storage 1-2.4:1.0
[516311.739789] scsi 27:0:0:0: Direct-Access     Linux    File-Stor Gadget 0401 PQ: 0 ANSI: 2
[516311.740862] sd 27:0:0:0: Attached scsi generic sg1 type 0
[516311.741205] sd 27:0:0:0: [sdb] 16384 512-byte logical blocks: (8.38 MB/8.00 MiB)
[516311.845657] sd 27:0:0:0: [sdb] Write Protect is off
[516311.845661] sd 27:0:0:0: [sdb] Mode Sense: 0f 00 00 00
[516311.845880] sd 27:0:0:0: [sdb] Write cache: enabled, read cache: enabled, doesn't support DPO or FUA
[516311.956797]  sdb:
[516312.176534] sd 27:0:0:0: [sdb] Attached SCSI removable disk
[516332.849561] FAT-fs (sdb): utf8 is not a recommended IO charset for FAT filesystems, filesystem will be case sensitive!
mount
/dev/sdb on /media/kevinchen/800E-5429 type vfat (rw,nosuid,nodev,relatime,uid=1000,gid=1000,fmask=0022,dmask=0077,codepage=437,iocharset=utf8,shortname=mixed,showexec,utf8,flush,errors=remount-ro,uhelper=udisks2)
```
