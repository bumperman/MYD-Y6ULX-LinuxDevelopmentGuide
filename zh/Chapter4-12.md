# 4.12 I2C EEPROM 测试

本例程通过访问I2C1总线，对核心板上的EEPROM Flash(U15)读写。执行i2c_flash程序后，会先写入四个字节，再读出。第一个参数为EEPROM设备的从地址。

```
# ./i2c_flash /dev/i2c-1
Read back:0x55
Read back:0x66
Read back:0x77
Read back:0x88
```
