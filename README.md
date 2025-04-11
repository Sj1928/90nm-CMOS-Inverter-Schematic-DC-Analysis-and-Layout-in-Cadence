# Project Title: CMOS Inverter in 90nm Technology

## Table of Contents
1. [Introduction](#introduction)
2. [Why CMOS Inverter?](#why-cmos-inverter)
3. [CMOS Inverter Analysis (Pre-Layout)](#cmos-inverter-analysis-prelayout)
    1. [DC Analysis](#dc-analysis)
    2. [Transient Analysis](#transient-analysis)
    3. [DC Parametric Analysis](#dc-parametric-analysis)
4. [Layout](#layout)

## Introduction
This project was created after my second year of study. It involves designing a CMOS inverter in 90nm technology using Cadence, along with DC analysis and layout.

## Why CMOS Inverter?
Why CMOS Inverter?
While NMOS alone might be simpler, it leads to higher power consumption, poor noise immunity, and limited functionality. CMOS, combining both PMOS and NMOS, is more efficient, reliable, and scalable for modern digital circuits.
### Construction
A CMOS inverter is made up of two transistors:
-A PMOS transistor connected to Vdd (positive supply voltage)
-An NMOS transistor connected to Vss or GND (ground)
Both transistors share the same input voltage (Vin) at their gates, and the output (Vout) is taken from the connection point between the PMOS and NMOS.
![photo_2025-04-11_10-18-35](https://github.com/user-attachments/assets/a924e7ae-775d-431d-865c-5632584669d4)

Transistor as a Switch
- Off State: The transistor exhibits infinite resistance when Vgs < Vt.
- On State: The transistor has finite resistance when Vgs > Vt.

Working of CMOS Inverter
When Vin is High (Vin = Vdd):
- PMOS transistor: Turns OFF.
- NMOS transistor: Turns ON.

When Vin is Low (Vin = 0V):
- PMOS transistor: Turns ON.
- NMOS transistor: Turns OFF.

Current Flow in CMOS Inverter
When Vin = Vdd (High Input):
- A direct path exists between Vout and Vss.
- As a result, Vout = 0V (Logic Low).

When Vin = 0V (Low Input):
- A direct path exists between Vdd and Vout.
- As a result, Vout = Vdd (Logic High).




## CMOS Inverter Analysis (Pre-Layout)

**##schematic**
![image](https://github.com/user-attachments/assets/3a2af793-245b-46e0-9296-cac68e989322)


### DC Analysis
DC analysis would be used to plot a Voltage Transfer Characteristics (VTC) curve for the circuit. It will sweep the value of Vin from high to low to determine the working of circuit with respect to different voltage levels in the input. The following plot is observed when simulated :
![Screenshot 2025-04-11 105252](https://github.com/user-attachments/assets/57f152ed-93a5-4465-83f2-2e86edca2595)

| Parameter | Value         |
|-----------|---------------|
| Vol       | 570 nV        |
| Voh       | 999.775 mV    |
| Vil       | 280 mV        |
| Vih       | 511.54 mV     |

![vol voh vil vih vth](https://github.com/user-attachments/assets/560b9c01-1588-4e7d-9f28-72a7ad5fa974)

-VOH - Maximum output voltage when it is logic '1'.
-VOL - Minimun output voltage when it is logic '0'.
-VIH - Maximum input voltage that can be interpreted as logic '0'.
-VIL - Minimum input voltage that can be interpreted as logic '1'.
-Vth - Inverter Threshold voltage
**note : Vth should be at a value of VDD/2 for maximum noise margins**
But here Vth = 411.24 mV 
### Vth Depends on Transistor Sizes (W/L ratios)
-The inverter threshold (also called the switching point) is the input voltage at which the output equals the input.
-This point is affected by the width-to-length ratios (W/L) of the PMOS and NMOS transistors.
-If both transistors had equal drive strengths, Vth ≈ Vdd/2.

### Noise Margin
Noise Margin High (NMH) = V<sub>OH</sub> − V<sub>IH</sub>
= 999.775 mV − 511.54 mV = 488.235 mV

Noise Margin Low (NML) = V<sub>IL</sub> − V<sub>OL</sub>
= 280 mV − 0.00057 mV = 279.99943 mV ≈ 280 mV

| Parameter | Value       |
|-----------|-------------|
| NMH       | 488.235 mV  |
| NML       | 280 mV      |

### Transient Analysis
Propagation delay refers to the time it takes for a signal to propagate through a gate or inverter, from the input transition to the output transition.
#### In the case of a CMOS inverter, there are two key delays:
-tpHL (propagation delay, high-to-low) - Time for the output to go from high (Vdd) to low (0V).
-tpLH (propagation delay, low-to-high) - Time for the output to go from low (0V) to high (Vdd).
**One can do this using Markers manually like this :**
![Delay calculation using marker TPLH edge middle](https://github.com/user-attachments/assets/2a8ffbf0-2f78-43d9-94a2-02f55114f8f4)
**But Cadence Virtuoso provides Calculator tool which precisely calculates delay and various other parameters**
![propogation delay usimhg calculator](https://github.com/user-attachments/assets/4c06639c-cd64-49d0-9277-6790483a6526)


// ### DC Parametric Analysis
// This section explains the parametric DC analysis, where you evaluate different design parameters under various conditions.

## Layout
Layout is the physical representation of a circuit on silicon.
It defines how transistors are placed and connected using layers like:
-Diffusion (active area)
-Polysilicon (gate)
-Metal layers (wiring)
-Contacts/vias (connections between layers)
-N-well / P-well regions (for PMOS/NMOS placement)

![layout without label](https://github.com/user-attachments/assets/16598cf8-6f4f-48cf-977c-2b6c32606830)

### Adding Label to Layout : 
-Labels like Vin, Vout, Vdd, and GND help identify which wire or node connects to what signal.
 Without labels, your layout is just shapes — the tool doesn’t know what's what.
![layout](https://github.com/user-attachments/assets/d99acfe0-4962-41d4-8c5e-0ce970a27bb1)
