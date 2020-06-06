---
title: Embedded linux notes
weight: 3
bookToc: false
---

[Configuring I2C under Armbian running on OrangePi Zero](#i2cArmbian)  
[Fixing ```/dev/i2c``` permissions with groups and udev rules](#permissions)  
[Reading the BME-280 pressure and temperature sensor in python](#BME-280)`

## I2C under Armbian running on OrangePi Zero <a name="i2cArmbian"></a>

Enable i2c in your system, select the required masters:
```bash
sudo armbian-config
## navigate System --> hardware --> perform selection
## reboot system
```
![devSelection](/images/armbian_config_i2c.jpg)

Check if i2c masters are detected:

```bash
~$ ls /dev/ | grep i2c
i2c-0
i2c-1
i2c-2
```

Get i2c-tools and perform device dpip etection:
```bash
sudo apt install i2c-tools
```

Perform detection using /dev/i2c-0
```bash
ja@orangepi-r1:~$ sudo i2cdetect 0
WARNING! This program can confuse your I2C bus, cause data loss and worse!
I will probe file /dev/i2c-0.
I will probe address range 0x03-0x77.
Continue? [Y/n] Y
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:          -- -- -- -- -- -- -- -- -- -- -- -- --
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
70: -- -- -- -- -- -- 76 --
ja@orangepi-r1:~$
```

Dump all the contents of device 0x76 detected by master 0:

```bash
ja@orangepi-r1:~$ sudo i2cdump 0 0x76
No size specified (using byte-data access)
WARNING! This program can confuse your I2C bus, cause data loss and worse!
I will probe file /dev/i2c-0, address 0x76, mode byte
Continue? [Y/n] y
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f    0123456789abcdef
00: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00    ................
10: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00    ................
20: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00    ................
30: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00    ................
40: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00    ................
50: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00    ................
60: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00    ................
70: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00    ................
80: 93 70 90 3a 53 37 fd 00 5c 6e 70 68 18 fc 09 8e    ?p?:S7?.\nph????
90: 8e d6 d0 0b ac 13 2b 01 f9 ff 8c 3c f8 c6 70 17    ??????+??.?<??p?
a0: 00 00 b2 00 00 00 00 00 00 00 00 00 33 00 00 c0    ..?.........3..?
b0: 00 54 00 00 00 00 60 02 00 01 ff b2 13 60 03 00    .T....`?.?.??`?.
c0: 00 00 00 ff 00 00 00 00 00 00 00 00 00 00 00 00    ................
d0: 58 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00    X...............
e0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00    ................
f0: 00 00 00 00 00 00 00 80 00 00 80 00 00 00 00 00    .......?..?.....
ja@orangepi-r1:~$

```

## Fix ```/dev/i2c``` permissions with groups and udev rules <a name="permissions"></a>
Change the i2c devices permissions so sudo is not required. If one looks at the device permissions we can see that:
```bash
ja@orangepi-r1:~/bmp280-python/examples$ ls -l /dev/i2c-0
crw-rw---- 1 root i2c 89, 0 Jun  5 11:45 /dev/i2c-0
ja@orangepi-r1:~/bmp280-python/examples$
```
Create a file ```/etc/udev/rulse.d/i2c.rules``` and add the new rule:
```
KERNEL=="i2c-[0-9]*", GROUP="i2c"
```
Reload the rules:
```bash
ja@orangepi-r1:~$ sudo udevadm control --reload-rules && udevadm trigger
```

List all the groups that are defined in the system:
```bash
ja@orangepi-r1:~$ getent group | grep i2c
i2c:x:113:
ja@orangepi-r1:~$
```
If group i2c does not exist, create it:
```bash
sudo groupadd i2c
```
Finally, add the current user (in my case user "ja") to the i2c group and reboot.

```bash
ja@orangepi-r1:~$ sudo adduser ja i2c
Adding user `ja' to group `i2c' ...
Adding user ja to group i2c
Done.
ja@orangepi-r1:~$ sudo reboot
```

Shotgun approach will also work, but far from ideal: ```sudo chmod 777 /dev/i2c-0```

## Reading the BME-280 pressure and temperature sensor in python

Get python3 support, package installer and smbus package:
```bash
~$ sudo apt install python3 python3-pip python3-smbus
```

Install the bmp280 library implementing the communication protocol with the sensor via i2c:
```bash
sudo pip3 install bmp280
```
The authors of the library have good examples in their repository, clone it and navigate to the examples folder:
```bash
~$ git clone https://github.com/pimoroni/bmp280-python
```

```bash
ja@orangepi-r1:~/bmp280-python/examples$ ls
compensated-temperature.py  temperature-and-pressure.py
dump-calibration.py         temperature-forced-mode.py
relative-altitude.py
ja@orangepi-r1:~/bmp280-python/examples$
```

The script ```compensated-temperature.py``` uses the ```vcgencmd``` command to get information from the RaspberryPi GPU core, hence it is not applicable in armbian under OrangePi. The example scripts from the [pimoroni repo](https://github.com/pimoroni/bmp280-python/blob/master/examples/temperature-and-pressure.py) have a hardcoded bus selected: ```/dev/i2c-1``` as follows ```bus = SMBus(1)``` If the target i2c slave is connected to a different i2c master, modify this value accordingly.

You can run my script below, which gets the i2c channel and the delay as arguments.

```python
#!/usr/bin/env python

import sys, getopt, time
from bmp280 import BMP280
try:
    from smbus2 import SMBus
except ImportError:
    from smbus import SMBus

def main(argv):
    try:
        opts, args = getopt.getopt(argv,"c:d:",["--channel","--delay"])
    except getopt.GetoptError:
        print ('myTPreader -c channel_number -delay delay_seconds')
        sys.exit(2)
    for opt, arg in opts:
        if opt in ('-c','--channel'):
            selectedChannel = int(arg)
        if opt in ('-d','--delay'):
            delay = int(arg)

    bus = SMBus(selectedChannel)
    bmp280 = BMP280(i2c_dev=bus)

    while True:
        temperature = bmp280.get_temperature()
        pressure = bmp280.get_pressure()
        print('{:05.2f}*C,{:05.2f}hPa'.format(temperature, pressure))
        time.sleep(delay)

if __name__ == "__main__":
    try:
        main(sys.argv[1:])
    except KeyboardInterrupt:
        sys.exit(0)

```

To run it for example for channel 0 with a delay of 1 sencond between reads:
```bash
ja@orangepi-r1:~/bmp280-python/examples$ python3 myTPreader.py -c 0 -d 1
```

To do:
* Provide an argument to the script with the bus number -b #, the reading -t or -p or -tp and the sleep time -d 