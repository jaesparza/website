---
title: loopantenna
weight: 2
bookToc: false
katex: true
---

# Magnetic loop antennas for HF bands

* Description of the content
* Antenna dimensions
* Control units
* Limitations
* Advantages
* Applicability (7 - 28 MHz)

Consider how to structure the content here, might be a good idea to split the page in several ones:
* "Landing" page, containing a general description of the projects, the motivation and an explanation on how the contents are structured.
* A single page con theoretical considerations with all the formulae - reference to the github page.

Notes no tuning units
* Manual tuning - tests with broadcasting capacitors
* Driving stepper motors and reducing vibrations
* L2: Butterfly variable capacitor tuning unit
* L2: Vacuum capacitor tuning unit

Notes on controllers
* Wired stepper controller
* Wireless stepper controller
* L2: Wireless communications
* L2: PC software

Notes on antenna dimensions and constructions:
* Coax loop
* Bike rim loop
* Heliax/Cellflex cable loop
* Plumber's copper tube

Tests <br />
* Deployment
* Videos of operation

How to structure the rest of the content? Tests, disclamers, etc...

## Disclamer

The antennas described here can generate high intensity RF fields in their vecinity as well as develop high voltages. If you decide to build them, do it at your own risk.

<center>
<img src="../static/img/rf_hazard.jpg" alt="Your image title" width="150"/>&nbsp;&nbsp;
<img src="../static/img/voltage_hazard.gif" alt="Your image title" width="150"/>
</center>

## Motivation

## Theoretical considerations

Ketex is going to be needed, let's try it:  
   
{{< katex >}}
L_{loop} [Henry] \approx \mu_{0}\mu_{r}\cfrac{D}{2}\bigg[\ln\bigg(\cfrac{ 8D}{d}\bigg)-2 \bigg]
{{< /katex >}}

### Antenna dimension cancluations

### Reduction and tunning resolution

## Initial experiments

### Outer and inner loops
A coaxial cable-based magnetic loop is an excellent starting point to being experimenting and getting familiar with the working principles. These antennas are typically constructed with an outer loop made with a coaxial cable of size RG-213. Many builds keep the structure with PVC pipes. To hold the loop shape better it is best to choose a cable like LMR400 due to its rigidity. When mounting the loop, the inner conductor and the jacket shall be shorted for efficiency reasons. In my build I have done this in the female connectors instead of in the cable itsefl or the male connector. This is a safety measure, in case I reuse the outer loop at a later point.

### Capacitors
* It is very common to see these antennas being tuned with broadcasting type capacitors. There are no impediments to using butterfly capacitors other than availability and size. A possible reason for the widespread use of broadcasting type is their low price and the fact that they are easy to cannibalize from vintage radios.
* It is key not to touch the shaft of the capacitor when tunning the antenna. The proximity of the hand will affect the capacitance and therefore the tuning (this is known as "hand effect"). Even worse, if the antenna is in transmission, one can get an RF burn even at low power levels.
* A reduction gear is advisable so it is easier to tune the loop, otherwise it is very difficult to find the spot where SWR is the lowest. Vernier dials are a good option to implement such a reduction.

Advantages:
* Easy, cheap and fast to build and prototype.
* Good antennas for portable operation, they can be dismounted easily.

Disadvantages:
* Lower efficiency than loops using thicker outer tubes.
* Since these builds are normally made with broadcasting capacitors of small plate separation, TX power typically cannot go beyond 10 Watts.

### Inspiration
There are many builds on the internet, both DIY implementations as well as commercial. 
The most widesread model is the AlexLoop antenna

I believe everything started with the AlexLoop [Insert link here].

https://www.yo3ggx.ro/magloop/PortableMagLoopBuild_v1.0.pdf

## Mechanical construction
* Stepper motors NEMA17
* Stepper motor with reduction

### Air variable capacitor unit

### Vacuum variable capacitor unit

## Software design

### Wired control unit
* Controlling the stepper motors, real-time considerations

### Wireless control unit
#### Embedded software
#### PC software

## Hardware design

### Wired control unit

### Wireless control unit

## Tests
* Antenna mounts
* Adding common mode chockes

## Concluding remarks

### Further work
* NEC modelling
* Implement it with either a faster processor or with two arduino controllers.

### Commercial models
* MFJ
* INAC
* Ciro Mazzoni
* Alexloop
* Chameleon
* MLA-M/T
* Käferlein loop
### Will I build it again?

## References
* ARRL antenna handbook
* https://www.nonstopsystems.com/radio/pdf-ant/article-antenna-mag-loop-2.pdf