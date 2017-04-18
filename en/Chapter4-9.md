# 4.9 Test Audio

This example demonstrates the development onboard audio interface using the arecord/aplay program in Linux systems.

* Connect LINE IN(J16) interface on the development board PC Audio-Out via a 3.5mm AUX cable
* HEADPHONE(J14) connecte the speakers

The computer play an music file and board will record and replay it.

```
arecord -f dat -t wav test.wav
aplay -f dat test.wav
```
