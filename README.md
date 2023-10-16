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
Then, the simulation results for vdn > vdp and vdp > vdn are presented to verify the adequate performance of the Dynamic Comparator.
![Simulation results when vdn > vdp](./Images/Dynamic_Comparator_vdn_great_vdp.png)
![Simulation results when vdp > vdn](./Images/Dynamic_Comparator_vdp_great_vdn.png)

In both simulation results it can be observed that when the circuit is operating during the reset phase (clkc = '0'), the outputs an and ap of the opamp take the value of '1' (both signals have the same offset in the simulations, an in green is over ap, which is in pink). On the contrary, dp and dn take the value of '0'.
During the regeneration phase (clkc = '1'), when the input vdp is larger than vdn, the outputs of the latch dn and dp take the values '1' and '0', respectively. Whereas, when vdn is larger than vdn, dn and dp take the values '0' and '1', respectively.

### SAR Logic

The next three figures correspond to the flip-flop D used in the SAR logic, the SAR logic with the eleven flip-flops, and the testbench used to validate the performance of this block.
![D Flip-Flop used in the SAR Logic](./Images/SAR_Logic_D_FF.png)
Schematic with the 11 Flip-Flops.
![11 D Flip-Flops cascaded used in the SAR Logic](./Images/SAR_Logic.png)
Corresponding testbench of the SAR Logic.
![SAR Logic testbench](./Images/SAR_Logic_tb.png)





