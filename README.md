# CMOS VLSI Schmitt Trigger Design

## About The Project
[cite_start]This project involves the design and implementation of a Schmitt Trigger circuit in Integrated Circuit (IC) form using Cadence Virtuoso[cite: 4]. 

[cite_start]A Schmitt trigger operates similarly to a standard comparator but features dual threshold voltages for rising and falling input signals[cite: 5]. [cite_start]This hysteresis provides essential noise immunity for voltage values close to the threshold, preventing false output switching in the circuit[cite: 5].

### Design Specifications
The circuit was designed to meet the following parameters:
* [cite_start]**Technology Node:** 45nm [cite: 41]
* [cite_start]**Operating Voltage ($V_{DD}$):** 1.2V [cite: 17]
* **Upper Threshold ($V_{SPH}$):** 800 mV [cite: 18]
* **Lower Threshold ($V_{SPL}$):** 400 mV [cite: 19]
* **Load Capacitance ($C_{load}$):** 200 fF [cite: 20]

---

## Circuit Operation & Theoretical Analysis

The core functionality of the Schmitt trigger relies on feedback mechanisms to shift the threshold depending on the current state:

* **Low-to-High Transition ($0 \to 1$):** When the input is low, PMOS transistors M5 and M6 conduct, pulling the output to $V_{DD}$ (High)[cite: 32]. NMOS M3 starts conducting, bringing the node between M1 and M2 to $V_{DD}$[cite: 33]. As the input voltage rises, M1 begins to conduct, but M2 resists turning on because its source voltage is at $V_{DD}$[cite: 34]. A much higher gate voltage is required to turn M2 on and pull the output to ground, which establishes the upper threshold $V_{SPH}$[cite: 35].
* [cite_start]**High-to-Low Transition ($1 \to 0$):** Conversely, when the input is high, NMOS M1 and M2 conduct, pulling the output to ground[cite: 36]. [cite_start]PMOS M6 conducts, bringing the node between M3 and M4 to ground[cite: 36]. [cite_start]M5 then turns on, pulling the M4-M5 node to $V_{DD}$, meaning M4 requires a significantly higher gate-to-source voltage to conduct[cite: 37]. [cite_start]This sets the lower threshold $V_{SPL}$[cite: 38].

### Sizing and Equations
The sizing ratios were calculated using the following theoretical equations:

[cite_start]$$\frac{\beta_{1}}{\beta_{3}} = \left[\frac{VDD-V_{SPH}}{V_{SPH}-V_{THN}}\right]^{2}$$ [cite: 40]

[cite_start]$$\frac{\beta_{5}}{\beta_{6}} = \left[\frac{V_{SPL}}{VDD-V_{SPL}-V_{THP}}\right]^{2}$$ [cite: 40]

[cite_start]Given the nominal threshold voltages of $V_{thn} \simeq 612mV$ and $V_{thp} \simeq 555.37mV$ [cite: 42][cite_start], the target transistor ratios were calculated as $\frac{\beta_{1}}{\beta_{3}} = 4.52$ [cite: 43] [cite_start]and $\frac{\beta_{5}}{\beta_{6}} = 2.66$[cite: 46]. 

[cite_start]While most transistors utilized the minimum channel length of $L = 45nm$ allowed by the technology, $L_6$ was adjusted to $60nm$ to achieve optimal hysteresis results without excessively enlarging the widths of the other transistors[cite: 95, 96].

---

## Simulation Setup
Simulations were performed to verify the thresholds without being affected by transient time delays. 
* [cite_start]A DC sweep of the input voltage ($V_1$) was utilized instead of a transient triangular pulse[cite: 50].
* [cite_start]The input was swept from 0 to 1.2V using a hysteresis sweep configuration to capture both the high and low switching points in a single simulation pass[cite: 58].
* A fine step size of 0.2mV was chosen to strike a balance between high measurement resolution and simulation efficiency[cite: 59].

---

## Layout Design
The physical layout was drafted with a focus on strict optimization constraints:
* [cite_start]**Area Minimization:** The primary goal was to minimize the total area, silicon footprint, and the number of metal layers used[cite: 152].
* [cite_start]**Metal Routing:** Metal 1 (M1) was standard for power supplies and regular signal routing[cite: 155]. [cite_start]Metal 2 (M2) was utilized strictly where necessary to cross paths (e.g., crossing M1 lines) to avoid drawing excessively long silicon routing lines[cite: 153, 154].

---

## Authors
* [cite_start]**Karapatsias Nikolaos** (10661) [cite: 2]
* **Stergiopoulos Evangelos** (10711) [cite: 2]
* [cite_start]*Group 21* [cite: 3]
