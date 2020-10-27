---
title: Mag loop
weight: 40
bookToc: false
bookHidden: false
katex: false
---

# DIY Magnetic loop antenna for 20-10 m bands

A description of the most relevant aspects in the construction of one of my loops, covering hardware, sofware and mechanical aspects.

**It contains the tricky parts that I have learnt throughout the way...**

## Specifications
* Power rating: tested up to 100 Watts (theoretical is higher?)
* Bandwidth: TX 14 to 28 MHz
* Loop diameter: XX cm
* Tuning through vacuum capacitor with electronic remote control
* Hardware end-stop protection through absolute positioning
* Heavy-duty vertical support

## Bill of Materials
* ebay and aliexpress 3d printer materials
* regular tool shops
* regular electronic shops
* insert here links to the pdf of the datasheets https://github.com/jaesparza/Loop-controller/tree/master/doc

![antenna]() 
* Picture 1: Loop in the tripod

## Antenna construction

The outer loop of the antenna is made of cellflex/heliax cable (section 7/8"). The diameter of the outer loop is 88 cm (length 2.76 m). This kind of cable is used as transmission line in high-performance RF installations (e.g. mobile telephony stations). The purity of the copper is much higher if compared to the material used in plumbing copper pipes. Also, construction is considerably simplified as no soldering of loop sections is required (as needed when assembling octogonal-shaped antennas).

The inner loop is made of thick soild copper wire and has a diameter of 19 cm. It is the weakest part of the loop and for a more robust finish this should be replaced by an inner loop constructed with coax cable (RG-58 will suffice).

The vertical support of the anntena is a wooden stick, here it is important to emphasize that no metallic supports shall be used to hold the antenna, as they will affect its efficiency. The attachment of the loop to the wooden support is done through a PVC gardening pipe support. The antenna is held straight through a heavy-duty tripod for camping TV-sat antennas, available in e-bay. It is bulky but light and very solid, and considerably cheaper than a solid photography/hi-fi tripod. The wooden support is attached to the tripod using regular metalic mounting brackets.

In order to protect the tunning unit, an regular electricity box has been used. The loop terminals are inserted into the box and protected with cable glands. The same strategy has been used for the control cable, with a ruggedized RJ-45 connector.

## Tuning unit
The tuning unit is one of the parts where I have spent most of the design and prototyping time. The tuning capacitor is a vacuum-type soviet 100 pF capacitor of maximum rating 5 kV. A capacitor with higher capacitance could be used, resulting in higher bandwidth. However this comes at the price of higher costs, a bigger capacitor that requires higher torque to operate and the need for a more complex support. Also, the dimensions of the antenna would prevent it from achieving a high TX efficiency.

![mounted](/img/tunningUnitResized.jpg)
* Picture 2: Detail of the tuning unit

In order to be able to determine the capacitor position a multiturn potentiometer is used. Multiturns potentiometer typically have 10 turns from minimum to maximum resistance. The vacuum capacitor used in this build has 14 turns from minimum to maximum capacitance. Rotations have to be reduced so the tuning range is not mechanically constrained by the potentiometer rotation range. To that end, a timing belt and two pulleis of different size are used, achieving a 2:1 reduction ratio.

The timing belt and pulleis used are:
* Belt model 94XL, 10 mm width
* Small pulley diameter 15.66 mm, center hole 8 mm
* Big pulley diameter 31.83 mm, center hole 6 mm

The transmission between the stepper motor and the vacuum capacitor is implemented through a combination of two differnt types of couplings. **It is key that there is no electrical connection between the tuning capacitor shaft and anything else**. A detail of the transmission is seen in picture **XX**. The stepper motor shaft connects through a solid coupling to a solid aluminium shaft, where the small pulley is mounted. Following it there is a flexible plastic coupling that finally connects to the stepper motor shaft. Using a flexible coupling is, althought not required, highly recommended because it will compensate for small missalignments between the motor and the capacitor that otherwise would result in vibrations. If no suitable plastic couplings can be found, an alternative is to use a teflon shaft to connect stepper motor and vacuum capacitor. However and since these components are used in 3-d printers they are abundant on-line.

The components in the tuning unit are mounted on a plexiglass support. Plexiglass is a good material to work with, it can be cut easily with a fine vertical saw and filed for a nice finish. Select thick plexiglass (5mm) so it will keep the assemby in place even when high torque is needed to move the capacitor. When making the wholes in the plexiglass base, make sure they are a few mm bigger than what is needed and afterwards use washers for final assembly. This facilitate final adjustment and alignmnet (obvious if you are a mechanical engineer, not obvious if you are a software one).

The stepper motor is a key component that has to be selected carefully for this application. Factors that are especially important are step size, power rating and reduction. In order to operate the vacuum capacitor without any external reduction, I have chosen a NEMA 17, 200 steps/rotation with planetary reduction gear of 5:1. This gives me enough torque to move the capacitor as well as a smoother rotation.

**PRO tip**: I also tried a NEMA 17 400 steps stepper motor, which can successfully rotate the capacitor. However, this comes at the cost of much higher current draw (up to 700 mA) to achieve operation towards the end. I recommend using a stepper motor with reduction gear to stay within a comfortable margin of 150 mA of current in the motor windings. 

The stepper motor holding bracket has to be selected so it is compatible with the stepper with planetary reduction box, meaning that it shall be possible to use holding screws within 14mm from the center shaft. See for comparison regular holding bracket and holding bracket compatible with the gearbox.

![Holding brackets]()

## Electronic control

![ecu]()
* Picture 3: Detail of the electronic control unit
* Overview and fetures: speed, direciton control and position idication
* Transmission and coupling - resolution calculation
* The advantage of using a potentiometer, is that its value stays in place after power-off making it possible to read where it was left on power up.

## Driving the stepper motor
* microstepping for smoother operation - position lost when driver is disabled
* Enable/ disable: no torque holindg, no noise, no current draw.
* Configura max curretndraw properly idela, torge and less vibrations

## Hardware considerations
* Powering the board
* PCB configuration - jumper settings
* Motor enable at power-up fix
* HF noise in the control line - RC lowpass filter

## Software considerations
* Select operational mode butterfly cap vs vacuum capacitor 
* Go through the software and spot key aspects (rt constraints, configuration, etc...)
* sofware design, singleton, 

![noise]()

![filter]()

### Operation

## Build vs. buy

Learn, time, price