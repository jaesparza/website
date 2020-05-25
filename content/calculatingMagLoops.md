---
title: design calculations
weight: 3
bookToc: true
katex: true
---

# Magnetic loop design calculations

The formulae below models the behaviour of a magnetic loop. Additional models are used to estimate the radiation resistance and the inductance of a single-turn loop.
Although significant ammount of litterature exists on the subject (these antennas exists since the 60s), I still have not found a single, self-contained resource that facilitates all the calculations needed to design a small transmitting loop. This summary intends to fill that gap.

## Loop radiation resistance
The radiation resistance is determined by the following expression:  

{{< katex >}}
R_{r} = 3.12 \times 10^4 \bigg(\cfrac{NA}{\lambda ^ 2}\bigg)^2
{{< /katex >}}

As it can be seen, the radiation resistance is proportional to the square of the number of loops (quadratic growth). As a consequence higher losses are present in multi-loop antennas.

## Conductor AC resistance 
The conductor resistance is determined by:  

{{< katex >}}
R_{AC} = \cfrac{\rho \times l}{A_{eff}}
{{< /katex >}}

Where {{< katex >}}\rho{{< /katex >}} is the resistivity of the conductor, {{< katex >}}l{{< /katex >}}
 the length of the conductor and {{< katex >}}A_{eff}{{< /katex >}} the effective radiating area, defined as follows:

{{< katex >}}
A_{eff} = \delta \pi d 
{{< /katex >}}

{{< katex >}}d{{< /katex >}} is the diameter of the conductor (e.g. 0.01m section for RG-213 coaxial cable)  

Although the current in a conductor flows in the outer layers due to the skin effect, there is a degree of penetration where current flow takes place. This is defined by {{< katex >}}\delta {{< /katex >}}, the current penetration depth:

{{< katex >}}
\delta = \sqrt{\bigg(\cfrac{\rho}{\pi \times f \times \mu}\bigg)} 
{{< /katex >}}<br/>


## Single loop inductance

{{< katex >}}
L_{loop} [Henry] \approx \mu_{0}\mu_{r}\cfrac{D}{2}\bigg[\ln\bigg(\cfrac{ 8D}{d}\bigg)-2 \bigg]
{{< /katex >}}




## Additional equations
{{< katex >}} \mu{{< /katex >}}: Absolute permeability  
{{< katex >}} \mu_{r}{{< /katex >}}: Relative permeability  
{{< katex >}} \mu_{0}{{< /katex >}}: Permeability of free space  

{{< katex >}}
\mu = \mu_{0}\mu_{r}
{{< /katex >}}<br/>

Circle length {{< katex >}} l {{< /katex >}} and area {{< katex >}} A{{< /katex >}}:  
{{< katex >}}
l = 2\pi r
{{< /katex >}}  
{{< katex >}}
A = \pi r ^ 2
{{< /katex >}}


{{< katex >}}
\lambda = \cfrac{c}{f}
{{< /katex >}}

## Related information
These models are coming in different shapes from a variety of sources. The primary one is the ARRL antenna handbook. The handbook uses formulas in a dangerous mix of imperial and metric units (spacecrafts have been lost due to [that](https://www.latimes.com/archives/la-xpm-1999-oct-01-mn-17288-story.html)). When using metric unit the International System is not always used. Both issues are corrected in the formulas presented here.