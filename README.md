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

## Description of the main blocks

The main blocks that integrate the design presented above are:

1) Differential Capacitive DAC (blue rectangle).
2) Switches for sampling (red rectangle).
3) Bridge Capacitor (horizontal capacitor in the differential capacitive DAC).
4) Switches for tracking (green rectangle).
5) Dynamic Comparator (purple rectangle).
6) SAR Logic (grey square).

### Differential Capacitive DAC
The schematic of the capacitive DAC array is composed of 
