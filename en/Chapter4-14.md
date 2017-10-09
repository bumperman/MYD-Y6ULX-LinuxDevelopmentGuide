# 4.14 WiFi Test


The MYD-Y6ULX board has a 4G module.

## Hardware Connective

Use I-PEX interface of wireless antenna connect with J24 position of board.

## Client Mode

The Client mode means WiFi module as client device connect to your route or other AccessPoint device.

Our Linux prebuilt system has added driver of WiFi module.It will be auto loaded when system startup.
And also use lsmod to confirm it.The wlan0 network device has exist when driver loaded success.The ifconfig command can be used confirm it.
