---
title: loopantenna
weight: 2
bookToc: true
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
* High voltages
* RF safety

## Motivation

## Theoretical considerations

Ketex is going to be needed, let's try it:  
   
{{< katex >}}
L_{loop} [Henry] \approx \mu_{0}\mu_{r}\cfrac{D}{2}\bigg[\ln\bigg(\cfrac{ 8D}{d}\bigg)-2 \bigg]
{{< /katex >}}

### Antenna dimension cancluations

### Reduction and tunning resolution

## Initial experiments
* Coax-based antennas - Alexloop clones

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