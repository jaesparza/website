---
title: Mag loop
weight: 40
bookToc: false
bookHidden: false
katex: false
---

### Specifications
* Power rating: tested up to 100 Watts
* Bandwidth: TX 14 to 28 MHz
* Loop diameter: XX cm
* Tuning through vacuum capacitor with electronic remote control
* Hardware end-stop protection through absolute positioning

![antenna]() 
* Picture 1: Loop in the tripod

### Tuning unit

![mounted](/img/tunningUnitResized.jpg)
* Picture 2: Detail of the tuning unit

Description
* Build description
* Components potentiometer, vacuum capacitor wall through 
* Custom pieces in plexiglass
* Stepper motor selection
* Transmission and coupling - resolution calculation

### Electronic control

![ecu]()
* Picture 3: Detail of the electronic control unit
* Overview and fetures: speed, direciton control and position idication
#### Driving the stepper motor
* microstepping for smoother operation - position lost when driver is disabled
* Enable/ disable: no torque holindg, no noise, no current draw.
* Configura max curretndraw properly idela, torge and less vibrations

### Hardware considerations
* Powering the board
* PCB configuration - jumper settings
* Motor enable at power-up fix
* HF noise in the control line - RC lowpass filter

### Software considerations
* Select operational mode butterfly cap vs vacuum capacitor 
* Go through the software and spot key aspects (rt constraints, configuration, etc...)
* sofware design, singleton, 

![noise]()

![filter]()

### Operation

