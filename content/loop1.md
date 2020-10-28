---
title: Mag loop
weight: 40
bookToc: false
bookHidden: false
katex: false
---

# Magnetic loop antenna for 20-10 m bands

In this page I describe the most relevant aspects in the construction of one of my loops to operate in the 20 to 10m bands (14 MHz to 28 MHz). I cover antenna mechanical construction, hardware, software and mechanical perspectives. Simply put, this is a compilation of details that I have learnt over this project and that I wish that somebody would have told me in the beginning. It is the hope that this will encourage future builders and facilitate the construction of quality loops.

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

![antenna in tripod]() 
* **Picture 1: Loop in the tripod**

## Antenna construction

The outer loop of the antenna is made of cellflex/heliax cable (section 7/8"). The diameter of the outer loop is 88 cm (length 2.76 m). This kind of cable is used as transmission line in high-end RF installations (e.g. mobile telephony stations). The purity of the copper is much higher if compared to the material used in plumbing copper pipes. Also, construction is considerably simplified as no soldering of loop sections is required (as needed when assembling octogonal-shaped antennas).

The inner loop is made of thick soild copper wire and has a diameter of 19 cm. It is the weakest part of the loop and for a more robust finish this should be replaced by an inner loop constructed with coax cable (RG-58 will suffice).

The vertical support of the anntena is a wooden stick, here it is important to emphasize that no metallic supports shall be used to hold the antenna, as they will affect its efficiency. The attachment of the loop to the wooden support is done through a PVC gardening pipe support. The antenna is held straight through a heavy-duty tripod for camping TV-sat antennas, available in e-bay. It is bulky but light and very solid, and considerably cheaper than a solid photography/hi-fi tripod. The wooden support is attached to the tripod using regular metalic mounting brackets.

In order to protect the tunning unit, an regular electricity box has been used. The loop terminals are inserted into the box and protected with cable glands. The same strategy has been used for the control cable, with a ruggedized RJ-45 connector.

## Tuning unit
The tuning unit is one of the parts where I have spent most of the design and prototyping time. The tuning capacitor is a vacuum-type soviet 100 pF capacitor of maximum rating 5 kV. A capacitor with higher capacitance could be used, resulting in higher bandwidth. However this comes at the price of higher costs, a bigger capacitor that requires higher torque to operate and the need for a more complex support. Also, the dimensions of the antenna would prevent it from achieving a high TX efficiency.

![mounted](/img/tunningUnitResized.jpg)
* **Picture 2: Detail of the tuning unit**

In order to be able to determine the capacitor position a multiturn potentiometer is used. Multiturns potentiometer typically have 10 turns from minimum to maximum resistance. The vacuum capacitor used in this build has 14 turns from minimum to maximum capacitance. Rotations have to be reduced so the tuning range is not mechanically constrained by the potentiometer rotation range. To that end, a timing belt and two pulleis of different size are used, achieving a 2:1 reduction ratio.

The timing belt and pulleis used are:
* Belt model 94XL, 10 mm width
* Small pulley diameter 15.66 mm, center hole 8 mm
* Big pulley diameter 31.83 mm, center hole 6 mm

The transmission between the stepper motor and the vacuum capacitor is implemented through a combination of two differnt types of couplings. **It is key that there is no electrical connection between the tuning capacitor shaft and anything else**. A detail of the transmission is seen in picture **XX**. The stepper motor shaft connects through a solid coupling to a solid aluminium shaft, where the small pulley is mounted. Following it there is a flexible plastic coupling that finally connects to the stepper motor shaft. Using a flexible coupling is, althought not required, highly recommended because it will compensate for small missalignments between the motor and the capacitor that otherwise would result in vibrations. If no suitable plastic couplings can be found, an alternative is to use a teflon shaft to connect stepper motor and vacuum capacitor. However and since these components are used in 3-d printers they are abundant on-line.

![transmission]()
* **Picture of the shaft**

The components in the tuning unit are mounted on a plexiglass support. Plexiglass is a good material to work with, it can be cut easily with a fine vertical saw and filed for a nice finish. Select thick plexiglass (5mm) so it will keep the assemby in place even when high torque is needed to move the capacitor. When making the wholes in the plexiglass base, make sure they are a few mm bigger than what is needed and afterwards use washers for final assembly. This facilitate final adjustment and alignmnet (obvious if you are a mechanical engineer, not obvious if you are a software one).

The stepper motor is a key component that has to be selected carefully for this application. Factors that are especially important are step size, power rating and reduction. In order to operate the vacuum capacitor without any external reduction, I have chosen a NEMA 17, 200 steps/rotation with planetary reduction gear of 5:1. This gives me enough torque to move the capacitor as well as a smoother rotation.

**PRO tip**: I also tried a NEMA 17 400 steps stepper motor, which can successfully rotate the capacitor. However, this comes at the cost of much higher current draw (up to 700 mA) to achieve operation towards the end. I recommend using a stepper motor with reduction gear to stay within a comfortable margin of 150 mA of current in the motor windings. 

The stepper motor holding bracket has to be selected so it is compatible with the stepper with planetary reduction box, meaning that it shall be possible to use holding screws within 14mm from the center shaft. See for comparison regular holding bracket and holding bracket compatible with the gearbox. Brackets compatible with steppers with gearbox are a bit less common but still possible to find at good prices from Chinese resellers.

![holdingBracket]()
* **Picture holding brackets for stepper motor**

## Electronic Control Unit (ECU)

The ECU is responsible for: 
* Driving the stepper motor at two diffrent speeds and in clockwise and counter-clockwise directions.
* Reading the capacitor position and displaying it on the LCD screen.
* Stopping the movement of the stepper if approaching the mechanical limits.

![ecu]()
* **Picture 3: Detail of the electronic control unit**

The two core components in the ECU are an **arduino pro micro** to run the control software and an **Allegro A4988** to facilitate stepper motor control. The rest of the hardware components are common passive, push buttons and connectors. The PCB is a two layer board that I designed using easyEDA (free on-line CAD tool) and produced through jlcPCB. PCB designs are available in the project repository under [pcb/initialPrototype](https://github.com/jaesparza/Loop-controller/tree/master/pcb/initialPrototype).


## Driving the stepper motor
Diring the stepper motor for optimal operation is a key aspect for succesful antenna usage. Speed has to be carefully determined so it is possible to change the bands fast while making it also possible to fine tune the antenna to achieve low SWR. The speed can be determined experimentally by playing with different pulse frequencies and duty cycles. Depending on target speed and selected stepper, a progressive acceleration will be needed. A function generator with TTL output can greatly help on determining the optimal driving frequency without constant compilation/deployment/testing cycles.

In addition to speed, carefully adjusting the following aspects wil greatly improve performance:
* **Microstepping** will allow for smooth stepper roation. The stepper driver used in this project is configured to a 16 step reduction. This is a fixed configuration via dip switches, but it could be programmable if desired via GPIOs.
* **Disable driver when not rotating** is a MUST. It will avoid noise in the radio receiver and it will decrease current draw considerably. Therefore, the enable line in the driver has to be toggled in the motor driver.
* **Tune maximum current** so microstepping works correctly and the motor does not exert more torque than necessary. It will decrease the heat disipated in the stepper motor driver and also decrease de vibrations in the mechanical assembly.

Based on the above, the following considerations apply to this specific application:
* In this build a 200 steps stepper motor with a 1:5 gearbox is used, therefore and accounting for the microstepping configuration: 16 micro_steps/step * 200 steps/motor_rotation * 5 motor_rotation/out_shaft = 8000 micro_steps/motor_rotation
* Due to the way microstepping works, if no torque is held, the position achived through microstepping will be lost. In this application this is acceptable.

**WARNING** do not disconnect the motor while the driver is powered and especially if the motor is rotating or holding torque, else the driver will be damaged.

## Hardware considerations
* Powering the board
* PCB configuration - jumper settings
* Motor enable at power-up fix
* HF noise in the control line - RC lowpass filter

## Software considerations
* Select operational mode butterfly cap vs vacuum capacitor 
* Go through the software and spot key aspects (rt constraints, configuration, etc...)
* sofware design, singleton, 
* With these needs in mind and for simplicity the controller is based on an Arduino pro mini and programmed in C++. 

![noise]()

![filter]()

### Operation

## Build vs. buy

Learn, time, price