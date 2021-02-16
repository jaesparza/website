---
title: multimode beacon
weight: 1
bookToc: false
---

# A low-power radio beacon for CW, QRSS and WSPR digital modulation.

A description of my multimode radio beacon for HF data transmissions. This beacon is simple to build with readily available and cheap components. It is a TX-only device and does not require other external radio equipment.

Specifications:
* TX in any amateur band between 160m to 10m (1.5 to 28 MHz).
* Filtered RF output of 200 mW.
* Easily programmable in Cpp with custom messages and operation.
* Internal RTC synchronized to GPS time for WSPR operation.


{{< hint danger >}}
Warning: Tx in amateur radio bands requires an amateur radio license. If you experiment in ISM bands instead make sure that you are allowed to do so. Comply with local radio and EMC regulations!
{{< /hint >}}



Software and notes on beacon configuration are availabe in the project [GitHub repository](https://github.com/jaesparza/radio-beacon).

Generating your custom WSPR message [link](https://github.com/jaesparza/radio-beacon/tree/main/sw/beacon#configure-your-won-wspr-frame)

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


![Test transmission of a WSPR frame](https://raw.githubusercontent.com/jaesparza/radio-beacon/main/doc/images/WSPR.PNG)

![Decoding the test transmission](https://raw.githubusercontent.com/jaesparza/radio-beacon/main/doc/images/rxWSJT-X.PNG)

![](https://raw.githubusercontent.com/jaesparza/radio-beacon/main/doc/images/amplifierOut.png)

## Supported modes

### QRSS
### WSPR
### CW (good old morse code)

## 