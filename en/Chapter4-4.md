# 4.4 Test GPIO-KEY

This example demonstrates how to read key state and key values in Linux user space. After running the gpio_key program, press or release the K3 key, the debug serial port will output the relevant status information. Press "Ctrl-C" to end the program.

- Run the program on board:

```
# ./gpio_key /dev/input/event2
Hit any key on board ......
key 2 Pressed
key 2 Released
key 2 Pressed
key 2 Released
```

