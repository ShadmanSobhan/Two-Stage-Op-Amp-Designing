# 1-V, High-Gain, Wide-Bandwidth Two-Stage Op-Amp
In this repository, the basic theory, design, layout, and results of two stage differential Op-Amp are discussed.

## Design

**Figure 1: Circuit Design**

<img src="Images/OTA Design.png" width="1000">

The OTA uses current mirror techniques, differential pairs with PMOS as the active load, Miller Compensation, a 600 µA current source, a supply voltage of $1V \pm 10\%$, and a common-source output stage.

The current source I1 flows through the diode-connected transistor N1, creating a reference voltage. This voltage is mirrored to N2, which provides a stable tail current for the differential pair (N4, N5).

N4 and N5 form an NMOS differential pair that converts the differential input voltage (Input<sup>+</sup> − Input<sup>−</sup>) into differential currents. P1 and P2 form a PMOS current mirror active load, converting the differential currents into a single-ended output current. This stage provides high gain and converts voltage to current (transconductance, $g_{m}$).

P3 (PMOS) acts as a common-source amplifier driven by the first stage. N3 (NMOS) serves as the current source load for P3. This stage provides additional voltage gain and drives the output load.

R1 ($50~\Omega$) and C1 (585fF) form the compensation network connected between the output and the intermediate node. This creates a dominant pole to ensure stability by moving the dominant pole to lower frequencies, introducing a zero (nulling resistor R1) to cancel the RHP zero. C2 (10pF) represents the load capacitance that the OTA must drive.

**Table 1: Transistor Dimensions**

| Name | Purpose                          | L (nm) | W_finger (um) | Multiplier | Fingers |
|------|----------------------------------|--------|---------------|------------|---------|
| N1   | Current Mirror                   | 500    | 5             | 8          | 6       |
| N2   | Tail Current Source              | 500    | 5             | 12         | 6       |
| N3   | Gain Stage NMOS                  | 500    | 5             | 52         | 6       |
| N4   | Input Differential Pair (-)      | 500    | 5             | 12         | 6       |
| N5   | Input Differential Pair (+)      | 500    | 5             | 12         | 6       |
| P1   | Active Load PMOS                 | 500    | 5             | 12         | 6       |
| P2   | Active Load PMOS                 | 500    | 5             | 12         | 6       |
| P3   | Gain Stage PMOS                  | 250    | 5             | 100        | 6       |

**Table 2: OTA Performance Parameters**

| Parameter | Definition | Equation |
|----------|------------|----------|
| Gain (Av) | Ratio of output voltage change to input voltage change | $A_v = \frac{V_\text{out}}{V_\text{in}}$ |
| Unity-Gain Bandwidth (UGB) | Frequency where gain becomes 1; determines speed | $f_t \approx \frac{g_m}{C_L}$ |
| Phase Margin (PM) | Measure of feedback stability | $\text{PM} = 180^\circ + \text{phase(open-loop)}$ |
| Power Supply Rejection Ratio (PSRR) | Ability to reject supply variations | $\text{PSRR} = \frac{dV_\text{DD}}{dV_\text{out}}$ |
| Input-Referred Noise (vn) | Equivalent input noise producing observed output noise | $v_n \approx \frac{V_\text{out,noise}}{A_v}$ |
| Slew Rate (SR) | Maximum rate of change of output voltage | $\text{SR} = \frac{dV_\text{out}}{dt}$ |
| Power Consumption | Total power used by OTA | $P = V_\text{DD} \cdot I_\text{DD}$ |
| Offset Voltage (Vos) | Input voltage required to make output zero | $V_\text{os} = V_\text{in}^+ - V_\text{in}^-$ |
| Total Harmonic Distortion (THD) | Ratio of harmonic power to fundamental | $\text{THD} = \frac{V_2 + V_3 + \dots}{V_1} \cdot 100%$ |
| Input Common-Mode Range (ICMR) | Valid input common-mode voltage range | --- |

## Corner Cases Tested
To evaluate the robustness of the designed OTA, we tested it under a total of **90 corner cases**, including:

**Process Variations (5 cases):**
- FF: Fast NMOS / Fast PMOS
- FS: Fast NMOS / Slow PMOS
- SF: Slow NMOS / Fast PMOS
- SS: Slow NMOS / Slow PMOS
- NN: Nominal NMOS / Nominal PMOS

**Voltage Variations (3 cases):**
- Typical: $V_\text{DD} = 1~\text{V}$
- Low: $V_\text{DD} = 0.9~\text{V}$
- High: $V_\text{DD} = 1.1~\text{V}$

**Temperature Variations (3 cases):**
- Very low: $-40^\circ\text{C}$
- Nominal: $25^\circ\text{C}$
- Extremely high: $125^\circ\text{C}$

**Input Common-Mode Range (ICMR):**
- $0.3V_\text{DD}$ to $0.8V_\text{DD}$


## Pre-Layout Simulation Results

**Table 3: Nominal Values and Process Variation before Layout**

| Parameters | Nominal | FF | SS | FS | SF |
|-----------|--------|----|----|----|----|
| Gain (dB) | 61.82 | 61.25 | 62.43 | 61.79 | 61.72 |
| UGB (MHz) | 137.2 | 157.4 | 114.8 | 143.1 | 125.1 |
| Phase Margin (deg) | 60.48 | 55.93 | 63.86 | 56.2 | 63.88 |
| PSRR (dB) | -64.43 | -63.94 | -65.15 | -65.2 | -63.73 |
| Input Referred Noise (µV) | 915.1 | 926.9 | 889.3 | 869.2 | 982.3 |
| Total Power (mW) | 5.945 | 5.935 | 5.952 | 6.184 | 6.184 |
| Slew Rate (V/µs) | 120.6 | 136.8 | 106.7 | 118.4 | 120.6 |
| Offset (µV) | -74.5 | -164 | 37.41 | -173.5 | 41.54 |

---

**Table 4: Supply Voltage Variation before Layout**

| Parameters | VDD-10% | VDD+10% |
|-----------|----------|----------|
| Gain (dB) | 61.79 | 61.83 |
| UGB (MHz) | 135.4 | 138.8 |
| Phase Margin (deg) | 60.36 | 60.58 |
| PSRR (dB) | -64.33 | -64.48 |
| Input Referred Noise (µV) | 920.9 | 911.5 |
| Total Power (mW) | 5.251 | 6.653 |
| Slew Rate (V/µs) | 113.8 | 122.4 |
| Offset (µV) | -164.8 | -278.5 |

---

**Table 5: Temperature Variation before Layout**

| Parameters | -40°C | 125°C |
|-----------|--------|--------|
| Gain (dB) | 61.2 | 61.5 |
| UGB (MHz) | 161.8 | 112.4 |
| Phase Margin (deg) | 62.35 | 59.92 |
| PSRR (dB) | -63.72 | -64.22 |
| Input Referred Noise (µV) | 844.1 | 1002 |
| Total Power (mW) | 5.777 | 6.062 |
| Slew Rate (V/µs) | 122.9 | 118.1 |
| Offset (µV) | -219.6 | 78.61 |

---

**Table 6: ICMR Variation before Layout**

| Parameters | 0.3 × VDD | 0.8 × VDD |
|-----------|-----------|-----------|
| Gain (dB) | 62.11 | 59.91 |
| UGB (MHz) | 113.8 | 141.5 |
| Phase Margin (deg) | 59.2 | 60.79 |
| PSRR (dB) | -64.02 | -59.37 |
| Input Referred Noise (µV) | 948.2 | 857.7 |
| Total Power (mW) | 5.419 | 6.079 |
| Offset (µV) | -108.3 | -42.55 |

## Layout

The total area required for the layout is approximately 0.01566 mm².

**Figure 2: Layout of the Designed OTA**

<img src="Images/Layout.png" width="1000">

**Figure 3: Placement of the MOSFETs**

<img src="Images/Layout_Split.png" width="1500">

## Post-Layout Simulation & Comparison of Before and After PEX

**Table 7: Nominal Values and Process Variation after PEX Simulation**

| Parameters | Nominal | FF | SS | FS | SF |
|-----------|--------|----|----|----|----|
| Gain (dB) | 61.43 | 60.78 | 62.3 | 61.48 | 61.23 |
| UGB (MHz) | 135.1 | 153.1 | 113.9 | 140.5 | 123.3 |
| Phase Margin (deg) | 57.7 | 52.45 | 61.81 | 53.26 | 61.4 |
| PSRR (dB) | -64.77 | -64.25 | -65.53 | -66.01 | -63.75 |
| Input Referred Noise (V) | 1.049 | 1.084 | 1.019 | 1.033 | 1.091 |
| Total Power (mW) | 6.173 | 6.272 | 6.041 | 6.308 | 6.014 |
| Slew Rate (V/µs) | 118.6 | 134.4 | 104.6 | 117.7 | 117 |
| Offset (µV) | 409.6 | 357.4 | 476.5 | 505.3 | 339.4 |

---

**Table 8: Supply Voltage Variation after PEX Simulation**

| Parameters | VDD-10% | VDD+10% |
|-----------|----------|----------|
| Gain (dB) | 61.4 | 61.44 |
| UGB (MHz) | 133.2 | 136.7 |
| Phase Margin (deg) | 57.6 | 57.78 |
| PSRR (dB) | -64.82 | -64.73 |
| Input Referred Noise (V) | 1.058 | 1.043 |
| Total Power (mW) | 5.456 | 6.906 |
| Slew Rate (V/µs) | 109.1 | 121.5 |
| Offset (µV) | 367.4 | 448.8 |

---

**Table 9: Temperature Variation after PEX Simulation**

| Parameters | -40°C | 125°C |
|-----------|--------|--------|
| Gain (dB) | 60.91 | 60.62 |
| UGB (MHz) | 160.4 | 110 |
| Phase Margin (deg) | 58.86 | 57.73 |
| PSRR (dB) | -64.21 | -64.04 |
| Input Referred Noise (V) | 0.939 | 1.199 |
| Total Power (mW) | 6.157 | 6.119 |
| Slew Rate (V/µs) | 121.4 | 115.4 |
| Offset (µV) | 278.7 | 610.5 |

---

**Table 10: ICMR Variation after PEX Simulation**

| Parameters | 0.3 × VDD | 0.8 × VDD |
|-----------|-----------|-----------|
| Gain (dB) | 61.81 | 61.43 |
| UGB (MHz) | 106.6 | 135.1 |
| Phase Margin (deg) | 56.96 | 57.7 |
| PSRR (dB) | -63.65 | -70.38 |
| Input Referred Noise (V) | 1.073 | 0.991 |
| Total Power (mW) | 5.586 | 6.244 |
| Offset (µV) | 107.4 | 295.9 |

**Table 11: Performance Comparison Before and After PEX**

| Parameters | Pre-Layout Minimum | Pre-Layout Maximum | Post-Layout Minimum | Post-Layout Maximum |
|-----------|------------------|------------------|-------------------|-------------------|
| Gain (dB) | 56.56 | 62.8 | 54.3 | 62.45 |
| UGB (MHz) | 51.15 | 198.1 | 48.11 | 192.5 |
| Phase Margin (Degrees) | 55.1 | 66.39 | 52.61 | 63.41 |
| Power Supply Rejection Ratio (PSRR) (dB) | -64.38 | -56.25 | -80.19 | -43.78 |
| Input Referred Noise (µV) | 739.1 | 1077 | 846 | 1279 |
| Slew Rate (V/µs) | 94.85 | 141.3 | 88.56 | 141.3 |
| Source Voltage Power (mW) | 2.233 | 6.403 | 2.361 | 6.75 |
| Current Source Power (µW) | 347.1 | 519.8 | 344.8 | 517.5 |
| Total Power (mW) | 2.581 | 6.923 | 2.706 | 7.258 |
| Offset Voltage (µV) | -819.1 | 96.63 | -770.9 | 804.9 |
| Total Harmonic Distortion (%) | 0.08695 | 1.86 | 0.1974 | 1.742 |

## Application of the Designed OTA
In this study, we considered mainly 10 parameters. Some results were satisfactory, while others were less optimal due to trade-offs. Our main design goal for this OTA was to achieve satisfactory gain, UGB, low noise, and THD while maintaining stability and a high phase margin.

The gain, slew rate, stability, THD, and PSRR achieved across all corners are good for an OTA. The average UGB is 100–150 MHz, but in some corners, the UGB became too high or too low. For example, in the SS corner at `-125°C`, the UGB measured `48.11 MHz` after PEX simulation. However, this is still acceptable as the OTA is designed for a `10 MS/s` SAR ADC.

For an `N`-bit SAR ADC with full-scale `V_FS = 1 V`, the LSB size is:
`LSB_N = V_FS / 2^N`

Hence:  
- `LSB_8 = 1 / 256 ≈ 3.906 mV`  
- `LSB_9 = 1 / 512 ≈ 1.953 mV`  
- `LSB_10 = 1 / 1024 ≈ 0.9766 mV`  

The measured post-layout input-referred noise of the OTA is between `846 µV` and `1279 µV`, which corresponds approximately to:  
- `0.22–0.33 LSB` for 8-bit  
- `0.43–0.66 LSB` for 9-bit  
- `0.87–1.31 LSB` for 10-bit operation  

Therefore, the OTA noise is comfortably low for 8-bit, acceptable for 9-bit SAR operation, but marginal-to-exceeding the 1-LSB budget at 10 bits (worst-case > 1 LSB).

To maintain high gain and UGB at low supply voltage, a high current was required to drive a `10 pF` load. This increased the required power for OTA operation, which is on average `3.5–5 mW`. One of the key design trade-offs is this higher power requirement.

The achieved offset voltage, which ranges up to approximately `±0.8 mV` across process, voltage, and temperature (PVT) variations, corresponds roughly to:  
- `0.2 LSB` for 8-bit  
- `0.4 LSB` for 9-bit  
- `0.8 LSB` for 10-bit resolutions  

This level of offset is negligible for 8-bit operation, acceptable for 9-bit accuracy, but borderline for 10-bit systems.


