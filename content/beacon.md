---
title: multimode beacon
weight: 1
bookToc: false
---

# A low-power radio beacon for CW, QRSS and WSPR digital modulation.

*A description of my multimode radio beacon for HF data transmissions. This beacon is simple to build with readily available and cheap components. It is a TX-only device and does not require other external radio equipment. Its applications are real-time HF propagation monitoring and antenna performance evaluation.*

## Specifications
* TX in any amateur band between 160m to 10m (1.5 to 28 MHz).
* Filtered RF output of 200 mW.
* Programmable in Cpp with custom messages and TX duty cycle.
* Internal STM32 RTC synchronized to GPS network time for WSPR operation.

## Foreword on low power
Many people are skeptical about the distances that can be accomplished with just 200mW of RF power. I was myself, until I built and put this radio beacon on the air. The map below shows all the stations that reported receiving my station (OU2ECV in the north of Europe), when transmitting at 200mW with my [loop antenna]({{< relref "../loop1.md" >}}) __inside my apartment__ using WSPR mode in the 20m band.

![Decoding the test transmission](https://raw.githubusercontent.com/jaesparza/radio-beacon/main/doc/images/contacts1.PNG)

## Overview

### Hardware 

The main hardware blocks are the following:
* **STM32 "Blue pill"**: is the controller board mounting a STM32 microcontroller with the minimal circuitry for it to function. It also carries the crystal needed by the internal RTC.
* **GPS**: is an external GPS module that can provide NMEA strings through a serial interface to the controller. It provides time and position information.
* **AD9850 DDS oscillator**: generates the FSK or CW modulated signal in the required frequency as controlled by the STM32.
* **Power amplifier**: provides a gain of XXdB to the oscillator output signal.
* **Low pass filter**: fiters out undesired harmonics from the power amplifier output.

During programming and developmet a ST-link dongle and a Serial to USB TTL cable are also needed.

```
* Schematics
    -> FIGURE:
* AD9850 output (5 volts)
* BS170 amplifier
    -> FIGURE: Measurements at 10/14 MHz
* Filter
    -> FIGURE: Harmonics before/after filtering
```
### Software

The control software is written in Cpp and uses the STM32duino abstraction layer. The software is structured in the following classes:

* **QRSS**: is a base class contining the common operations for QRSS operation: message transmission, morse encoding and also access to the oscillator.
* **FSK Sender** and **CW Sender**: are subclasses of QRSS that implement Frequency Shift Keying CW and traditional morse code respectively.
* **WSPR**: implements the WSPR encoding using the four-level FSK.
* **TimeSync**: maintains a local notion of time synchronized to the GPS network. The STM32 internal RTC is synchronized to the time values provided by the GPS through NMEA strings. Triggers the transmission when scheduled through RTC alarm attached interrupt.

The controls software uses the following libraries:
* **AD8850**: controls the DDS oscillator. Based on the library from [R. Tilard](https://github.com/RobTillaart/AD985X), modified to: use a configurable SPI interface and added a calibration method.
* **TinyGPSPlus**: interfaces the GPS and parses the NMEA strings. The library contains methods for positioning and navigation however, only time functionality is used. Library from [Mikal Hart](https://github.com/mikalhart/TinyGPSPlus).

Software and notes on beacon configuration are availabe in the project [GitHub repository](https://github.com/jaesparza/radio-beacon).

## WSPR Operation

### Setup
Before putting the beacon on the air, the following setup is needed:
1. Determine the band in which the beacon is going to transmitt and plug the appropriate low pass filter for that band.
2. Generate the WSPR message that will be sent by the beacon by following the instructions [link](https://github.com/jaesparza/radio-beacon/tree/main/sw/beacon#configure-your-won-wspr-frame) An example of a WSPR message can be seen in the code listing below. Replace the contents of the `uint8_t MY_WSPR_DATA` array.
3. Set the desired TX duty cycle in minutes.
4. Recompile and flash.

```C
/*
 * Example message from the WSPR user manual
 *
 * The standard format according to the protocol spec. is: "callsign + 4-digit
 * locator + dBm"
 * Channel symbols for the message "K1ABC FN42 37"
 */
uint8_t EXAMPLE_WSPR_DATA[] = {
    3, 3, 0, 0, 2, 0, 0, 0, 1, 0, 2, 0, 1, 3, 1, 2, 2, 2, 1, 0, 0, 3, 2, 3,
    1, 3, 3, 2, 2, 0, 2, 0, 0, 0, 3, 2, 0, 1, 2, 3, 2, 2, 0, 0, 2, 2, 3, 2,
    1, 1, 0, 2, 3, 3, 2, 1, 0, 2, 2, 1, 3, 2, 1, 2, 2, 2, 0, 3, 3, 0, 3, 0,
    3, 0, 1, 2, 1, 0, 2, 1, 2, 0, 3, 2, 1, 3, 2, 0, 0, 3, 3, 2, 3, 0, 3, 2,
    2, 0, 3, 0, 2, 0, 2, 0, 1, 0, 2, 3, 0, 2, 1, 1, 1, 2, 3, 3, 0, 2, 3, 1,
    2, 1, 2, 2, 2, 1, 3, 3, 2, 0, 0, 0, 0, 1, 0, 3, 2, 0, 1, 3, 2, 2, 2, 2,
    2, 0, 2, 3, 3, 2, 3, 2, 3, 3, 2, 0, 0, 3, 1, 2, 2, 2,
};
```
### Dry run
A QRSS viewer software can be used to test the beacon operation before connecting it to an antenna. An option is [ARGO QRSS viewer](https://digilander.libero.it/i2phd/argo/). This test requires a HF receiver and a digital modes interface, so the audio signal can be fed into the PC's soundcard. An example of a correct full WSPR frame that can be decoded is shown below. The critical aspect here is that the separation between the tones that are transmitted looks correct (approximately, sicne this viewer does not have a high resolution).

![Test transmission of a WSPR frame](https://raw.githubusercontent.com/jaesparza/radio-beacon/main/doc/images/WSPR.PNG)

An additional and final method to check that data framing is correct, is to use the [WSJT-X official software](https://www.physics.princeton.edu/pulsar/k1jt/wsjtx.html) and check that the preprogrammed message in the beacon is successfully decoded. Below an example of several succesful decodifications for the message "OU2ECV JO65 23" - which indicates OU2ECV transmitting from locator JO65 (Copenhagen) with 23 dBm (200 mW).

![Decoding the test transmission](https://raw.githubusercontent.com/jaesparza/radio-beacon/main/doc/images/rxWSJT-X.PNG)

### Final words before transmitting

{{< hint danger >}}
Warning: The PA FET can and will get hot. Attach a heatsink/adopt the necessary precautions.
{{< /hint >}}

{{< hint danger >}}
Warning: Trasmission in amateur radio bands requires an amateur radio license. Comply with local radio and EMC regulations!
{{< /hint >}}


## Build vs. buy

