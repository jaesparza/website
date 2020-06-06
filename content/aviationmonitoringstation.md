---
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

Common measurement conditions
* Ambient temperature of:
* Two bm280 taking measurements every second
* Armbianmonitor measureming CPU die temperature and system load

Sensor placement:
* one BME-280 sensor in direct contact through a thermal sticker to the RTL-SDR dongle metal case.
* one BME-280 sensor measuring temperature inside the waterproof box.
* one sensor in the die.

Idle state:
* 1 x RTL sdr connected,
* system booted and idle
* average current draw of 145 mA

System receiving in the VHF airband
* 1 x RTL sdr connected,
* system in RX
* rtl_tcp running
* average current draw of 