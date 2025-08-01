# RC Phase Shift Oscillator (100 kHz)

## Project Overview

This project implements a single-stage RC Phase Shift Oscillator using a BJT (Bipolar Junction Transistor) to generate a stable sinusoidal waveform at approximately 100 kHz. The design was simulated using LTspice and then built and tested on a breadboard.

## For Detailed Report, Visit
https://gamma.app/docs/Analog-Circuits-Lab-Design-Projects-Group-5-h3c633m2n0gn635?mode=doc

## Introduction

An RC phase shift oscillator is a type of electronic oscillator that generates a sinusoidal output waveform. It utilizes a feedback network consisting of resistors and capacitors to produce the necessary phase shift and gain for oscillation. This project focuses on a common emitter BJT configuration for amplification, combined with a three-stage RC ladder network to provide a 180-degree phase shift, meeting the Barkhausen criterion for sustained oscillations.

## Theory of Operation

The Barkhausen stability criterion states that for sustained oscillations, two conditions must be met:

1.  **Loop Gain:** The magnitude of the loop gain (product of amplifier gain and feedback network attenuation) must be equal to or greater than unity.
2.  **Phase Shift:** The total phase shift around the loop must be an integer multiple of 360 degrees.

In a common emitter BJT amplifier, there's an inherent 180 degree phase shift between the input and output. To achieve a total 360 degree phase shift, the feedback network must introduce an additional 180 degree phase shift. A three-stage RC ladder network is typically used, where each RC stage contributes approximately 60 degree of phase shift at the oscillation frequency.

The BJT amplifier provides the necessary gain to compensate for the attenuation introduced by the RC phase shift network, ensuring the loop gain condition is met.


## Components Used

BC547B ,100pf (3 units),0.01uf,1nf,0.1uf,6.8k ohm(3 units),10k ohm,100k ohm(2 units),2.2k ohm,1k ohm(2 units)

*Note: Specific resistor and capacitor values will depend on your design to achieve 100 kHz. Please refer to the LTspice simulation file for exact values.*
## Design Aspects
## 1. Establishing the DC Operating Point (Q-Point)
The first step in the design is to establish a stable DC operating point, or Q-point, for the transistor. This ensures the amplifier operates in the active region and can produce a large, undistorted output signal.

Initial Specifications
The design starts with the selection of the transistor and the initial operating conditions:



Transistor: BC107 


Transistor Gain (h 
fe
​
  or β): 110 


Supply Voltage (V 
CC
​
 ): 12 V 


Quiescent Collector Current (I 
C
​
 ): 2 mA 

Component Calculation

Collector-Emitter Voltage (V 
CE
​
 ): To allow for maximum symmetrical swing of the output signal, the quiescent V 
CE
​
  is set to 50% of the supply voltage. 


V 
CE
​
 =0.50×V 
CC
​
 =0.50×12V=6V 


Emitter Resistor (R 
E
​
 ): The voltage across the emitter resistor (V 
RE
​
 ) is set to 10% of V 
CC
​
  for thermal stability. 


V 
RE
​
 =0.10×V 
CC
​
 =0.10×12V=1.2V 

Using Ohm's law and assuming the emitter current (

I 
E
​
 ) is approximately equal to the collector current (I 
C
​
 ), R 
E
​
  is calculated:



R 
E
​
 = 
I 
C
​
 
V 
RE
​
 
​
 = 
2mA
1.2V
​
 =600Ω 

The nearest standard resistor value selected is 

560 Ω. 


Collector Resistor (R 
C
​
 ): The voltage drop across the collector resistor (V 
RC
​
 ) is determined by applying Kirchhoff's Voltage Law to the collector-emitter loop:


V 
RC
​
 =V 
CC
​
 −V 
CE
​
 −V 
RE
​
 =12V−6V−1.2V=4.8V 


The resistance for R 
C
​
  is then calculated:


R 
C
​
 = 
I 
C
​
 
V 
RC
​
 
​
 = 
2mA
4.8V
​
 =2.4kΩ 

The nearest standard resistor value selected is 

2.2 k$\Omega$. 

## 2. Designing the Voltage Divider Biasing Network
A voltage divider bias network, consisting of resistors R 
1
​
  and R 
2
​
 , is used to set the proper DC base voltage (V 
B
​
 ).

Base Current (I 
B
​
 ): The base current is calculated using the collector current and the transistor's gain (β):


I 
B
​
 = 
β
I 
C
​
 
​
 = 
110
2mA
​
 ≈18.2μA 


Base Voltage (V 
B
​
 ): The base voltage is the sum of the voltage across the emitter resistor and the base-emitter forward voltage drop (V 
BE
​
 ), which is assumed to be 0.6 V. 


V 
B
​
 =V 
RE
​
 +V 
BE
​
 =1.2V+0.6V=1.8V 


Biasing Resistors (R 
1
​
  and R 
2
​
 ): To ensure a stable bias, the current flowing through resistor R 
2
​
  (I 
2
​
 ) is chosen to be ten times the base current (I 
B
​
 ).

The value for 

R 
2
​
  is calculated as:


R 
2
​
 = 
10×I 
B
​
 
V 
B
​
 
​
 = 
10×18.2μA
1.8V
​
 =9.9kΩ 

The nearest standard value of 

10 k$\Omega$ is selected for R 
2
​
 . 

The current through 

R 
1
​
  (I 
1
​
 ) is the sum of the current through R 
2
​
  and the base current, which is 11×I 
B
​
 . The value for 

R 
1
​
  is calculated as:


R 
1
​
 = 
11×I 
B
​
 
V 
CC
​
 −V 
B
​
 
​
 = 
11×18.2μA
12V−1.8V
​
 ≈51kΩ 

The nearest standard value of 

47 k$\Omega$ is selected for R 
1
​
 . 

## 3. Designing the AC Circuit Components
Capacitors are added to couple the AC signal and bypass the emitter resistor, shaping the amplifier's frequency response. The design targets a lower cutoff frequency of 200 Hz. 

Input Coupling Capacitor (C 
C1
​
 ): This capacitor couples the input signal while blocking DC. Its reactance (

X 
C1
​
 ) should be at most 1/10th of the amplifier's input impedance (R 
in
​
 ) at the lower cutoff frequency. 

The input impedance 

R 
in
​
  is calculated as the parallel combination of R 
1
​
 , R 
2
​
 , and the transistor's input impedance (h 
fe
​
 ×r 
e
​
 , where r 
e
​
  is assumed to be 12.5 Ω), resulting in R 
in
​
 =1.17kΩ. 


X 
C1
​
 ≤ 
10
1.17kΩ
​
 =117Ω 


C 
C1
​
 = 
2πfX 
C1
​
 
1
​
 = 
2π×200Hz×117Ω
1
​
 ≈6.8μF 

A standard value of 

10 μF is selected. 

Output Coupling Capacitor (C 
C2
​
 ): This capacitor couples the amplified signal to the next stage. Its reactance (

X 
C2
​
 ) should be at most 1/10th of the output resistance (R 
out
​
 ), which is approximately R 
C
​
  (2.2 k$\Omega$).


X 
C2
​
 ≤ 
10
2.2kΩ
​
 =220Ω 


C 
C2
​
 = 
2πfX 
C2
​
 
1
​
 = 
2π×200Hz×220Ω
1
​
 ≈3.6μF 

A standard value of 

3.3 μF is selected. 

Emitter Bypass Capacitor (C 
E
​
 ): This capacitor is used to bypass the emitter resistor for AC signals, thus maximizing the voltage gain. Its reactance (

X 
CE
​
 ) should be at most 1/10th of R 
E
​
  at the lowest operating frequency. 


X 
CE
​
 ≤ 
10
560Ω
​
 =56Ω 


C 
E
​
 ≥ 
2πfX 
CE
​
 
1
​
 = 
2π×200Hz×56Ω
1
​
 ≈14.2μF 

A standard value of 

22 μF is selected to ensure good bypassing

## Simulation (LTspice)

The circuit was first simulated in LTspice to verify its functionality and optimize component values for the target frequency of 100 kHz.


## Breadboard Implementation

The simulated circuit was then assembled on a breadboard. Careful attention was paid to component placement and wiring to minimize parasitic capacitances and inductances that could affect performance at 100 kHz.


## Results

The breadboarded RC phase shift oscillator successfully generated a near-sinusoidal waveform at approximately 100 kHz.

### Measured Output Waveform

**Observed Frequency:** \~100 kHz (Slight variations from theoretical are expected due to component tolerances and breadboard parasitics).
**Observed Amplitude:** [State the peak-to-peak or RMS amplitude you measured]

## Troubleshooting & Notes

  * **No Oscillation:**
      * Check all connections for proper contact.
      * Ensure the BJT is correctly biased (Q-point in active region).
      * Verify the gain of the amplifier stage is sufficient (adjust collector resistor).
      * Check for correct component values (especially RC network).
      * Ensure the feedback loop is closed correctly.
  * **Distorted Output:**
      * The amplifier might be saturating or cutting off due to improper biasing.
      * Gain might be too high, leading to clipping.
      * Parasitic capacitances on the breadboard can distort the waveform at higher frequencies. Try to keep connections short and neat.
  * **Frequency Shift:**
      * Component tolerances (resistors and capacitors) greatly affect the output frequency. Using precision components can help.
      * Temperature variations can also cause slight frequency drift.
  * **Breadboard Limitations:** Prototyping on a breadboard introduces parasitic capacitance and inductance, which can become significant at higher frequencies (like 100 kHz), potentially affecting the waveform shape and stability. For more stable and cleaner output, a PCB implementation would be recommended.

## Future Enhancements

  * **Frequency Tuning:** Implement a variable resistor or capacitor in the RC network to allow for frequency adjustment.
  * **Amplitude Control:** Add a variable resistor in the feedback path or an AGC (Automatic Gain Control) circuit for stable amplitude.
  * **Buffer Stage:** Add a buffer (e.g., an op-amp voltage follower) at the output to isolate the oscillator from the load and prevent frequency/amplitude changes when a load is connected.
  * **PCB Design:** Design and fabricate a custom Printed Circuit Board (PCB) for a more robust and cleaner output, minimizing parasitic effects.
  * **Harmonic Filtering:** Implement a low-pass filter at the output to further reduce any higher-order harmonics and produce a purer sine wave.
