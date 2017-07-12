# 4.11 Test USB OTG

This example demonstrates use of the USB OTG(J7) interface of the development board to simulate a specified file or device as a Gadget device. It works as a storage device to the HOST device.

- Operation steps on board:

```
mkfs.vfat /dev/ram1
insmod g_mass_storage.ko file=/dev/ram1 removable=1 \
iSerialNumber="1234"

[ 3048.950498] Mass Storage Function, version: 2009/09/11
[ 3048.982245] LUN: removable file: (no medium)
[ 3048.997849] LUN: removable file: /dev/ram1
[ 3049.000674] Number of LUNs=1
[ 3049.002272] Number of LUNs=1
[ 3049.023990] g_mass_storage gadget: Mass Storage Gadget, 
version: 2009/09/11
[ 3049.029682] g_mass_storage gadget: g_mass_storage ready
[ 3094.766373] g_mass_storage gadget: high-speed config #1: 
Linux File-Backed Storage

```
- The host PC display a USB device connected and SerialNumber is "1234":

```
dmesg | tail -n 20
[2872436.778616] usb 1-1: USB disconnect, device number 102
[2872436.779156] sd 3:0:0:0: [sdb] Synchronizing SCSI cache
[2872436.779201] sd 3:0:0:0: [sdb] Synchronize Cache(10) failed:
Result: hostbyte=DID_NO_CONNECT driverbyte=DRIVER_OK
[2872442.508567] usb 1-1: new high-speed USB device number 103 
using xhci_hcd
[2872442.650549] usb 1-1: New USB device found, idVendor=0525, 
idProduct=a4a5
[2872442.650551] usb 1-1: New USB device strings: Mfr=3, 
Product=4, SerialNumber=5
[2872442.650552] usb 1-1: Product: Mass Storage Gadget
[2872442.650553] usb 1-1: Manufacturer: Linux 4.1.15-1.2.0+g8d98
da6 with 2184000.usb
[2872442.650554] usb 1-1: SerialNumber: 1234
[2872442.657827] usb-storage 1-1:1.0: USB Mass Storage device 
detected
[2872442.657895] usb-storage 1-1:1.0: Quirks match for vid 0525 
pid a4a5: 10000
[2872442.657923] scsi host3: usb-storage 1-1:1.0
[2872443.669426] scsi 3:0:0:0: Direct-Access     Linux    File-
Stor Gadget 0401 PQ: 0 ANSI: 2
[2872443.669886] sd 3:0:0:0: Attached scsi generic sg1 type 0
[2872443.670820] sd 3:0:0:0: [sdb] 131072 512-byte logical 
blocks: (67.1 MB/64.0 MiB)
[2872443.779976] sd 3:0:0:0: [sdb] Write Protect is off
[2872443.779979] sd 3:0:0:0: [sdb] Mode Sense: 0f 00 00 00
[2872443.890093] sd 3:0:0:0: [sdb] Write cache: enabled, 
read cache: enabled, doesn't support DPO or FUA
[2872444.110372]  sdb:
[2872444.330074] sd 3:0:0:0: [sdb] Attached SCSI removable disk

```
