# Introduction

This repository is going store the modified driver I have met.

## ADT7490

This is a chip for doing thermal monitor and fna control.

Reference:
* Specification: https://www.analog.com/media/en/technical-documentation/data-sheets/adt7490.pdf
* The cuurent status from Linux: https://docs.kernel.org/hwmon/adt7475.html
* The current code from linux repo: https://github.com/torvalds/linux/blob/master/drivers/hwmon/adt7475.c

The summary from Linux doc:
* ADT7490:
  * 6 voltage inputs
  * 1 Imon input
  * PECI support (not implemented)
  * 2 GPIO pins (not implemented)  <------------------- Target, modified.
  * system acoustics optimizations (not implemented)

The modification here:
* Support the accessiblity of two GPIO pins, GPIO1/GPIO2.

Code:
* [adt7490](drivers/hwmon/adt7475.c)

Example:

```shell
$ cd /sys/class/hwmon/hwmon2
$ ls gpio* -l
-rw-r--r--    1 root     root          4096 Jun 26 10:13 gpio1_direction
-rw-r--r--    1 root     root          4096 Jun 27 01:14 gpio1_polarity
-rw-r--r--    1 root     root          4096 Jun 27 01:15 gpio1_value
-rw-r--r--    1 root     root          4096 Jun 26 10:13 gpio2_direction
-rw-r--r--    1 root     root          4096 Jun 27 01:14 gpio2_polarity
-rw-r--r--    1 root     root          4096 Jun 27 01:15 gpio2_value
$ echo 1 > gpio1_polarity
$ echo 1 > gpio1_value  (Turn on LED)
$ echo 0 > gpio1_value  (Turn off LED)
```
