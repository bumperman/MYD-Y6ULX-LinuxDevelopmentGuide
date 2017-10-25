# 4.2 Test TouchPanel

This example shows you how to test the touch panel on LCD screen module. The MYD-Y6ULX supports capacitive and resistive type.You need follow 4.1 to install the LCD module.

You can use ts_calibrate and ts_test command to test your LCD and touch panel are working.The "TSLIB_TSDEVICE" point the touch device node, capacitive and resistive has different device node.

```
# export TSLIB_TSDEVICE=/dev/input/event1
# ts_calibrate

# ts_test

```

