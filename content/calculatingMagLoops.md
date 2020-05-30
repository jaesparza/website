---
title: design calculations
weight: 3
bookToc: true
katex: true
---

# Magnetic loop design calculations

The formulae below models the behaviour of a magnetic loop, provides expressions to determine the radiation and AC resistance of a loop and estimate its inductance. Additionally, simple equations are provided to calculate the tuning capacitance taking parasitic capacitances into account.

All the expressions here use the International System of Units, if you want sensible results,  honor it  (spacecrafts are lost when people [do not](https://www.latimes.com/archives/la-xpm-1999-oct-01-mn-17288-story.html)).

## Equations specific to loop antennas
### Radiation resistance
The radiation resistance is determined by the following expression:  

{{< katex >}}
R_{r} = 3.12 \times 10^4 \bigg(\cfrac{NA}{\lambda ^ 2}\bigg)^2 \; [Ohms]
{{< /katex >}}


As it can be seen, the radiation resistance {{< katex >}} R_{r} {{< /katex >}} is proportional to the square of the number of loops {{< katex >}} N {{< /katex >}} and the area described by the loop {{< katex >}} A {{< /katex >}} As a consequence higher losses are present in multi-loop antennas. In the expression {{< katex >}} \lambda {{< /katex >}} is the signal wavelenght at a particular frequency.

### Single loop inductance
The loop inductance can be approximated by:  

{{< katex >}}
L_{loop} \approx \mu_{0}\mu_{r}\cfrac{D}{2}\bigg[\ln\bigg(\cfrac{ 8D}{d}\bigg)-2 \bigg] \: [Henry] 
{{< /katex >}}

Where {{< katex >}} D {{< /katex >}} is the loop diameter and {{< katex >}} d {{< /katex >}} is the diameter (section) of the conductor used to construct the loop. The constants for absolute permeability of vacuum {{< katex >}} \mu_{0}{{< /katex >}} and relative permeability of air {{< katex >}} \mu_{r}{{< /katex >}} are provided in the [constants](#constants) section.

### Distributed capacitance (MEDHURST?)

Any inductor has a parasitic capacitance and, when dimensioning a loop antenna, it is key to take it into consideration.
When calculating the maximum frequency at which the antenna is to operate, the distributed capacitance has to be added to the minimum capacitance that the tuning capacitor can reach. This determines the total tuning capacitance (C) that is applied to the loop to reach resonance. If this value is too high for the given loop dimensions, the loop lenght will have to be shortened such that the distributed capacitance decreases.

{{< katex >}}
C_{dist} = 0.82 \times l \;[Farads]
{{< /katex >}}

{{< hint warning >}}
Many loop antenna builds cannot reach the desired maximum frequency because the designers do not take into consideration the distributed capacitance. The distributed capacitance has to be added to the tuning capacitor minimum capacitance.
{{< /hint >}}

{{< katex >}}
C = C_{dist} + C_{tuning} \;[Farads]
{{< /katex >}}

For orientation, minimum capacitance values for butterfly capacitors can be between 10 - 30 pF. For soviet vacuum capacitors the minimum value I have seen is 4 pF.


## Conductor AC resistance
The conductor resistance is determined by:  

{{< katex >}}
R_{AC} = \cfrac{\rho \times l}{A_{eff}} \;[Ohms]
{{< /katex >}}

Where {{< katex >}}\rho{{< /katex >}} is the resistivity of the material the conductor is made of, {{< katex >}}l{{< /katex >}}
 the length of the conductor and {{< katex >}}A_{eff}{{< /katex >}} the effective radiating area, defined as follows:

{{< katex >}}
A_{eff} = \delta \pi d 
{{< /katex >}}

{{< katex >}}d{{< /katex >}} is the diameter of the conductor (e.g. 0.01m section for RG-213 coaxial cable)  

Although the current in a conductor flows in the conductor surface due to the [skin effect](https://en.wikipedia.org/wiki/Skin_effect), there is a degree of penetration where current flow takes place. This is defined by {{< katex >}}\delta {{< /katex >}}, the current penetration depth:

{{< katex >}}
\delta = \sqrt{\bigg(\cfrac{\rho}{\pi \times f \times \mu}\bigg)} 
{{< /katex >}}<br/>

Where {{< katex >}} \mu{{< /katex >}} is the absolute permeability and {{< katex >}} f {{< /katex >}} is the frequency at which  {{< katex >}}R_{AC}  {{< /katex >}} is evaluated.


## Radiation efficiency

Once {{< katex >}}R_{AC}{{< /katex>}} and {{< katex >}}R_{r}{{< /katex>}} have been established for the given loop dimensions, configuration, material and operating frequency, the radiation efficiency can be calculated as:

{{< katex >}}
\eta = \cfrac{R_{r}}{(R_{r} + R_{AC})} \times 100
{{< /katex>}}


## RLC circuit solutions

A loop antenna can be lump-modelled as a RLC system. Therefore, the following equations model its properties:

Quality factor:

{{< katex >}}
Q = \cfrac{f}{\Delta f} = \cfrac{X_{L}}{2(R_{r} + R_{AC})}
{{< /katex>}}<br/>

Capacitor voltage:

{{< katex >}}
V_{c} = \sqrt{P X_{L} Q}
{{< /katex>}}<br/>

Circulating current:

{{< katex >}}
I_{L} = \sqrt{\cfrac{P  Q}{X_{L}}}
{{< /katex>}}

{{< hint danger >}}
During transmission even at moderate power levels (e.g. 10 Watts) the capacitor voltage is within the range of kV and the circulating current are several Amps. If you are designing an antenna calculate these two parameters to a) select a tuning capacitor of adequate ratings and b) to understand the risks that these antennas might pose.
{{< /hint >}}

### Reactance

Inductive reactance: {{< katex >}}X_{L} = 2 \pi f L_{loop}{{< /katex >}}

Capacitive reactance: {{< katex >}}X_{C} = \cfrac{1}{2 \pi f C}{{< /katex >}}

When the antenna is resonant: <br/>

{{< katex >}} X_{L} = X_{C} \Rightarrow 2 \pi f L_{loop} = \cfrac{1}{2 \pi f C} \Rightarrow C = \cfrac{1}{4 \pi ^ 2 f^2 L_{loop}}{{< /katex >}}

{{< hint warning >}}
The capacitance C calculated above includes both the tunning capacitor AND the distributed capacitance.
{{< /hint >}}

## Basic equations

{{< katex >}} \mu{{< /katex >}}: Absolute permeability  
{{< katex >}} \mu_{r}{{< /katex >}}: Relative permeability  
{{< katex >}} \mu_{0}{{< /katex >}}: Permeability of free space  

{{< katex >}}
\mu = \mu_{0}\mu_{r}
{{< /katex >}}<br/>

Circle length {{< katex >}} l {{< /katex >}} and area {{< katex >}} A{{< /katex >}}:  

{{< katex >}}
l = 2\pi r 
{{< /katex >}}<br/>

{{< katex >}}
A = \pi r ^ 2
{{< /katex >}}  

Relation between frequency and wavelength  
{{< katex >}}
\lambda = \cfrac{c}{f}
{{< /katex >}}

## Symbols used in this document:  

||||
|:----|:----|:----|:----|
|{{< katex >}} R_{r} {{< /katex >}} | Radiation resistance|{{< katex >}} C_{tuning} {{< /katex >}}| tuning capacity |
|{{< katex >}}  N {{< /katex >}} | Number of turns|{{< katex >}}  R_{AC} {{< /katex >}}| AC resistance |
|{{< katex >}} A {{< /katex >}}| Area of the loop |{{< katex >}}  \Delta f{{< /katex >}}| Bandwidth|
|{{< katex >}}\lambda {{< /katex >}}| wavelength|{{< katex >}} f {{< /katex >}}| frequency|
|{{< katex >}}  L_{loop} {{< /katex >}}| Loop inductance |{{< katex >}} P  {{< /katex >}}| Power |
|{{< katex >}} \mu {{< /katex >}} | Absolute permeability| {{< katex >}}  X_{L} {{< /katex >}}| Inductive reactance |
|{{< katex >}}  D  {{< /katex >}}| Loop diameter |{{< katex >}}  X_{C} {{< /katex >}}| Capacitive reactance |
|{{< katex >}}d {{< /katex >}}| Conductor diameter | {{< katex >}} V_{c}  {{< /katex >}}| Capacitor voltage |
|{{< katex >}} C_{dist}{{< /katex >}}| Distributed capacitance | {{< katex >}} I_{L} {{< /katex >}}| Cirulating current |
|{{< katex >}} l {{< /katex >}}| lenght of the conductor|{{< katex >}} C {{< /katex >}}| Capacity|
|{{< katex >}} Q {{< /katex >}}| Quality factor|


## Constants

|{{< katex >}} \pi {{< /katex >}}|  {{< katex >}} 3.1415 {{< /katex >}}| {{< katex >}} \mu_{0}{{< /katex >}} | {{< katex >}} 4 \pi \times 10^{-7} \;[H/m] {{< /katex >}}| 
|:----|----:|:----|-----:|
| {{< katex >}} c {{< /katex >}} | {{< katex >}} 3 \times 10^{8} \;[m/s]{{< /katex >}}| {{< katex >}} \mu_{r \_ air}{{< /katex >}}  |  {{< katex >}} 0.99994 \; [H/m]  {{< /katex >}}|
| {{< katex >}} \rho_{copper} {{< /katex >}}|||

## Related information
Although significant ammount of litterature exist on the subject (these antennas exists since the 60s), I still have not found a single, self-contained resource that facilitates all the calculations needed to design a small transmitting loop. This summary intends to fill that gap.

These models are coming in different shapes from a variety of sources. The primary one is the ARRL antenna handbook. The handbook uses formulas in a dangerous mix of imperial and metric units. When using metric units, the International System is not always used. Both issues are corrected in the formulas presented here.