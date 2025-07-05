# RC Phase Shift Oscillator (100 kHz)

## Project Overview

This project implements a single-stage RC Phase Shift Oscillator using a BJT (Bipolar Junction Transistor) to generate a stable sinusoidal waveform at approximately 100 kHz. The design was simulated using LTspice and then built and tested on a breadboard.

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
