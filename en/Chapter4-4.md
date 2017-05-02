# 4.7 Test GPIO-GPIO

This example demonstrates how to read key state and key values in Linux user space. After running the gpio_key program, press or release the S2 key, the debug serial port will output the relevant status information. Press "Ctrl-C" to end the program.

- Run the program on board:

```
# ./gpio_key /dev/input/event0
Hit any key on board ......
key 260 Pressed
key 260 Released
key 260 Pressed
key 260 Released
```

