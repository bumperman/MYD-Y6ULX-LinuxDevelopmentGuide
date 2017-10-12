# 4.11 Test Audio

This example demonstrates the development onboard audio interface using the arecord/aplay program in Linux systems.


## Hareware connect

* Connect LINE IN(J5) interface on the MYB-6ULX board, PC Audio-Out via a 3.5mm AUX cable
* HEADPHONE(J4) connecte the your headerphone or speaker

## Software operation

The PC plays the audio file and execute arecord command on board.It will recored data and save to test.wav file.You can use "ctrl + c" stop it after one minute.
```
# arecord -f cd test.wav
```

Use aplay command to play file that previous step recoreded.
```
# aplay test.wav
```


