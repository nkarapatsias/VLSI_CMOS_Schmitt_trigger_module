# CMOS VLSI Schmitt Trigger Design

## About The Project
This repository contains the design and implementation of a Schmitt Trigger integrated circuit using the Cadence Virtuoso toolset. 

While functioning similarly to a standard comparator, a Schmitt trigger introduces hysteresis by providing two distinct threshold voltages: one for the rising edge and one for the falling edge. This characteristic offers critical noise immunity, particularly when input values hover close to the switching thresholds, thereby preventing false or erratic output transitions.

### Specifications
The circuit was designed based on the following target parameters:
* **Process Node:** 45nm
* **Supply Voltage ($V_{DD}$):** 1.2V
* **High Threshold ($V_{SPH}$):** 800 mV
* **Low Threshold ($V_{SPL}$):** 400 mV
* **Output Load Capacitance ($C_{load}$):** 200 fF

---

## Theoretical Analysis & Operation

The hysteresis in this circuit is achieved through an internal feedback mechanism that alters the switching threshold based on the output's current state:

* **Low-to-High Transition ($0 \to 1$):** With an initial low input, PMOS transistors M5 and M6 are in conduction, setting the output to $V_{DD}$. NMOS M3 turns on, pulling the intermediate node between M1 and M2 to $V_{DD}$. As the input voltage increases, M1 begins to conduct. However, M2 remains off because its source is tied to $V_{DD}$. A significantly higher gate voltage is required to force M2 into conduction and pull the output low, creating the upper switching threshold ($V_{SPH}$).
* **High-to-Low Transition ($1 \to 0$):** With an initial high input, NMOS M1 and M2 conduct, pulling the output to ground. PMOS M6 turns on, grounding the intermediate node between M3 and M4. This forces M5 to conduct, pulling the M4-M5 node to $V_{DD}$. Consequently, M4 requires a much larger gate-to-source voltage to turn on. This establishes the lower switching threshold ($V_{SPL}$).

### Sizing & Design Equations
The W/L ratios were derived using the following theoretical design equations:

$$\frac{\beta_1}{\beta_3} = \left( \frac{V_{DD} - V_{SPH}}{V_{SPH} - V_{THN}} \right)^2$$

$$\frac{\beta_5}{\beta_6} = \left( \frac{V_{SPL}}{V_{DD} - V_{SPL} - V_{THP}} \right)^2$$

Using the simulated threshold voltages ($V_{thn} \approx 612 mV$ and $V_{thp} \approx 555.37 mV$), the calculated ratios were approximately $\beta_1 / \beta_3 = 4.52$ and $\beta_5 / \beta_6 = 2.66$. 

While the majority of the design utilizes the minimum technology length of $L = 45nm$, the length of M6 was deliberately increased to $L_6 = 60nm$. This adjustment yielded superior hysteresis characteristics without necessitating excessive transistor widths elsewhere in the circuit.

---

## Simulation Approach
To isolate the voltage thresholds from transient time delays, DC simulations were prioritized: 
* The input voltage ($V_1$) was evaluated using a DC Sweep from 0V to 1.2V.
* A hysteresis sweep option was enabled to capture both the high and low switching points in a single, unified simulation pass.
* A step resolution of 0.2mV was utilized to maintain high precision without unnecessarily burdening the simulation engine.

---

## Physical Layout Optimization
The physical layout was drafted with strict rules for area and routing efficiency:
* **Area Reduction:** The design minimizes the overall silicon footprint and reduces active area usage.
* **Metal Layers:** Metal 1 (M1) was used for standard signal and power lines. Metal 2 (M2) was employed strictly for necessary cross-routing (such as crossing existing M1 traces) to avoid drawing highly resistive, extended poly-silicon lines.

---

## Authors
* **Karapatsias Nikolaos** (10661)
* **Stergiopoulos Evangelos** (10711)
* *Group 21*
