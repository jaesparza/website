--
title: air-traffic monitor
weight: 30
bookToc: false
bookHidden: false
---

# Aviation monitoring station

## Disclamer
* Legal limits, privacy considerations.
* Didactic purposes
* This is not designed to be an instrument for aerial navigation.

## Project scope
* ADSB
* ACARS
* VHF airband comms

## Hardware
### SDR radios
### Antennas and filters
### Embedded linux platform
### Assembly
* Waterproofing
* Power delivery
* Humidity and temperature sensor
## Software
### ADSB decoders
### ACARS decoders
### GNURADIO
### Extending data processing via socket
### Sensor interfacing
### Data storage and processsing
## Deployment and tests
## Commercial alternatives
## References
* Baalint seever videos
* Commander cat videos
* DEFCON talks


## Thermal considerations

The RTL-SDR dongles are known to reach high temperatures, up to 80 deg. C in some components. In the early versions of the dongles this issue was particularly bad. [S50LEA](http://lea.hamradio.si/~s57uuu/mischam/rtlsdr/thermal.htm) documented this issue and took thermal images of the system before and after adding a heathsink.

![thermal](https://www.rtl-sdr.com/wp-content/uploads/2015/10/rtlsdr_thermal_cam.jpg)

In this project, I was planning to set all the electronic hardware (voltage regulator, embedded linux board and at least one RTL-dongle) in a waterproof PCV box. Even though the dongle that I am using is a bit more modern than the one shown in the thermal image, thermal issues are still relevant. To assess how hot the whole setup gets while powered I have run a number of experiments. 

The following temperature sensors have been placed in the hardware:
* one BME-280 sensor in direct contact through a thermal sticker to the RTL-SDR dongle metal case.
* one BME-280 sensor measuring temperature inside the waterproof box.
* one sensor in the die.

All the measurements have been taken with the box exposed to an ambient temperature of 25.5 deg. C

I have developed a [python script]() to read periodically the temperature sensor and print the readings to stdout. [Armbianmonitor]() is used to monitor the cpu state. The measurement scripts are launched in three separate terminals as follows:
```bash
ja@orangepi-r1:~/$ python3 myTPreader.py -c 0 -d 1 | tee lidClosedIdle_inside

ja@orangepi-r1:~/$ python3 myTPreader.py -c 1 -d 1 | tee lidClosedIdle_sdr

ja@orangepi-r1:~/$ armbian -m | tee lidClosedIdle_die_Opi
```
### Measurements

Temperature measurements are collected when the system is in these two different states:

Idle state:
* 1 x RTL sdr connected
* system booted and idle
* average current draw of 200 mA @ 12V (2.4 Watts)

RX state - system receiving in the VHF airband:
* 1 x RTL sdr connected
* system in RX
* rtl_tcp running
* average current draw of XXX mA

#### Measurements without heatsinks

#### Measurements with heatsinks
