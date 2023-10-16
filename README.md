# 11-bit differential SAR ADC design

## Introduction

The proposed ADC-SAR design is presented in the following figure.

![ADC_SAR proposal](./Images/SAR_ADC.png)

The specifications that must be fulfilled are:

|Specification|Symbol|Baseline requirement|Comment|
|:--:|:--:|:----------:|:----------:|
|Sampling rate|fs|≥ 1.5MS/s|||
|Effective number of bits|ENOB|≥ 9|Measured near Nyquist|
|Input Capacitance|Cin|≤ 5pF||

We define the following values based on the architecture presented above:

- Vcm = Vdd/2​
- Vrefp = Vdd​
- Vrefn = 0

## Description and simulation results of the main blocks

The main blocks that integrate the design presented above are:

1) Differential Capacitive DAC (blue rectangle).
2) Switches for sampling (red rectangle).
3) Bridge Capacitor (horizontal capacitor in the differential capacitive DAC).
4) Switches for tracking (green rectangle).
5) Dynamic Comparator (purple rectangle).
6) SAR Logic (grey square).

### Differential capacitive DAC
The schematic of the capacitive DAC array comprises 10 capacitors connected in a bridged configuration to separate the most significant bits from the less significant bits. The unitary capacitor value is 100fF. (In progress to be optimized)
![Differential capacitive DAC schematic](./Images/Differential_capacitive_DAC_array_sch.png)

The corresponding symbol in xschem is presented below.
![Differential capacitive DAC symbol](./Images/Differential_capacitive_DAC_array.png)

### Bootstrap tracking switch
The schematic of the Bootstrap tracking switch is illustrated below. The main goal of this configuration is to avoid surpassing the breakdown voltage of the transistors that compose the architecture used for tracking.

Follows the testbench for the Bootstrap tracking switch
![Bootstrap tracking switch testbench](./Images/tracking_switches_tb.png)

The simulation results of Vgs and Vds for NMOS transistors and Vsg and Vsd for PMOS transistors that integrate the Bootstrap tracking switch are shown.
![Simulations of Vds and Vgs values for NMOS and PMOS transistors.](./Images/tracking_switch_sims.png)
It is possible to observe that none of the voltage values exceed 4.1V, which is smaller than the breakdown voltages of the transistors. (In progress to be optimized)

### Dynamic Comparator
Then, the schematic of the dynamic comparator composed of the opamp, the latch, the two inverters, and the nand can be observed.
![Dynamic Comparator schematic](./Images/Dynamic_Comparator.png)
Additionally, the corresponding testbench with the 180 degrees out of phase two inputs VDN and VDP.
![Dynamic Comparator testbench](./Images/Dynamic_Comparator_tb.png)
