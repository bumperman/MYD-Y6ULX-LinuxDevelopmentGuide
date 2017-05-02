# 4.2 Test TouchPanel

This example show you how to test the touch panel on LCD screen module. The MYS-6ULX supports capacitive and resistive type.We also have two LCD with touch panel module, MY-TFT070CV2 and MY-TFT043RV2.

You can use ts_calibrate and ts_test command to test your LCD and touch panel are working.The "TSLIB_TSDEVICE" point the touch device node, capacitive and resistive has difference device node.

```
export TSLIB_TSDEVICE=/dev/input/event1
# ts_calibrate

# ts_test

```

