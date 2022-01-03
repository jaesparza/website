---
title: coax mag-loop
weight: 2
bookToc: false
katex: true
bookHidden: true
---

# A lightweight coax-loop antenna
A coaxial cable-based magnetic loop is an excellent starting point to being experimenting and getting familiar with the working principles of magnetic loop antennas.

Advantages:
* Easy, cheap and fast to build and prototype.
* Good antennas for portable operation, they can be dismounted easily.

Disadvantages:
* Lower efficiency than loops using thicker outer tubes.
* Since these builds are normally made with broadcasting capacitors of small plate separation, TX power typically cannot go beyond 10 Watts.

## Outer and inner loops
The outer loop is typically made with a coaxial cable size RG-213. To hold the loop shape better it is best to choose a cable like LMR400 due to its rigidity. When mounting the loop, the inner conductor and the jacket shall be shorted for efficiency reasons. In my build I have done this in the female connectors instead of in the cable itself or the male connector. This is a safety measure, in case I reuse the outer loop at a later point. The inner loop needs to have a legth of 1/5 and 1/8 of the outer loop.  Finally, the transmitting loop is kept in many builds with a vertical piece of PVC tubing. Others also use coaxial cable for the vertical support (see CHA F-LOOP).

## Capacitors
It is very common to see these antennas being tuned with broadcasting type capacitors. There are no impediments to using butterfly capacitors other than availability and size. A possible reason for the widespread use of broadcasting type is their low price and the fact that they are easy to cannibalize from vintage radios.

It is key not to touch the shaft of the capacitor when tunning the antenna. The proximity of the hand will affect the capacitance and therefore the tuning (this is known as "hand effect"). Even worse, if the antenna is in transmission, one can get an RF burn even at low power levels.

A reduction gear is advisable so it is easier to tune the loop, otherwise it is very difficult to find the spot where SWR is the lowest. Vernier dials are a good option to implement such a reduction.

## My build

General specifications:

* Tunable between 7 to 30 MHz
* 1 meter diameter outer loop, made of LMR400. 1 cm cable section.
* The vertical support is made of PVC piping and it fits well on a photography tripod.

Specifications per band:

|                                               | 7 MHz     | 10 MHz    | 14 MHz    | 18 MHz  | 21 MHz   | 24 MHz   | 28 MHz    |
|-----------------------------------------------|-----------|-----------|-----------|---------|----------|----------|-----------|
| Efficiency                                    | 7%        | 21%       |  46%      | 67%     | 78%      | 85%      |  91%      |
| Bandwidth                                     | 13.4 kHz  | 18.8 kHz  |  32.6 kHz | 61 kHz  | 97.7 kHz | 152 kHz  |  265 kHz  |
| Tunning capacitance                           | 293 pF    | 144 pF    |  73 pF    | 44 pF   | 33pF     | 25 pF    |  18 pF    |
| Capacitory Voltage [RMS] @ 100 Watts          | 2013 V    | 2472 V    |  2579 V   | 2424 V  | 2236 V   | 2043 V   |  1809 V   |
| Circulating current @ 100 Watts               | 26 A      | 21.9 A    |  16.6 A   | 12.2 A  | 9.62A    | 7.69 A   |  5.83 A   |
| Capacitor Voltage [RMS] @ 5 Watts             | 450 V     | 543 V     |  577 V    | 542 V   | 500 V    | 457 V    |  404 V    | 
| Circulating current @ 5 Watts                 | 5.81 A    | 4.90 A    |  3.72 A   | 2.72 A  | 2.15 A   | 1.72 A   | 1.30 A    |

### Final comments

I have used this antenna both portable and in my apartment balcony extensively and with good results. This is an antenna that every loop experimenter should build, but potential purchase shall be carefully considered, as the existing models in the market are highly priced (as of 2020).

There are many builds on the internet, both DIY implementations as well as commercial. The most widesread model is the AlexLoop antenna but there are others, such as the Chameleon CHA F-LOOP 2.0. Many other hams have built similar antennas, a good inspiration and a well documented project can be found in [YO3GGX website](https://www.yo3ggx.ro/magloop/PortableMagLoopBuild_v1.0.pdf).