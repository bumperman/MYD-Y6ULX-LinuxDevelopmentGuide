# 4.8 Test GPIO-KEY

This example demonstrates using the Linux system API to operate two LED lights on the development board, D8 and D9. After running the program, D8 and D9 flash alternately. Press "Ctrl-C" to end the program.

```
# ./gpio_led /sys/class/leds/D8/brightness /sys/class/leds/D9/brightness
```

