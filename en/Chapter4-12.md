# 4.12 Test I2C EEPROM

This program reads and writes EEPROM Flash(U15) on the core board by accessing the I2C1 bus. After executing the i2c_flash program, four bytes are written and read. The first parameter is the slave address of the EEPROM device.

```
# ./i2c_flash /dev/i2c-1
Read back:0x55
Read back:0x66
Read back:0x77
Read back:0x88
```
