# 4.2 Test RTC

This example demonstrates the use of the Linux API to set and read the RTC on the development board. Copy the executable program rtc_test to the development board.

Setup current time to system:

```
# ./rtc_test -s 11 03 40 2014 08 14
date/time is updated to: 14-8-2014, 11:03:40.
```

Read time from system:

```
# ./rtc_test
Current RTC date/time is 14-8-2014, 11:03:50.
```

