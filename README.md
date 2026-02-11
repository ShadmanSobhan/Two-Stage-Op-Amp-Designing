# 1-V, High-Gain, Wide-Bandwidth Two-Stage Op-Amp
In this repository, the basic theory, design, layout, and results of two stage differential Op-Amp are discussed.

## Design
The design of our proposed OTA is shown in the following figure.

<img src="Images/OTA Design.png" width="500">

The OTA uses current mirror techniques, differential pairs with PMOS as the active load, Miller Compensation, a 600 µA current source, a supply voltage of $1V \pm 10\%$, and a common-source output stage.

The current source I1 flows through the diode-connected transistor N1, creating a reference voltage. This voltage is mirrored to N2, which provides a stable tail current for the differential pair (N4, N5).

N4 and N5 form an NMOS differential pair that converts the differential input voltage (Input<sup>+</sup> − Input<sup>−</sup>) into differential currents. P1 and P2 form a PMOS current mirror active load, converting the differential currents into a single-ended output current. This stage provides high gain and converts voltage to current (transconductance, $g_{m}$).

P3 (PMOS) acts as a common-source amplifier driven by the first stage. N3 (NMOS) serves as the current source load for P3. This stage provides additional voltage gain and drives the output load.

R1 ($50~\Omega$) and C1 (585fF) form the compensation network connected between the output and the intermediate node. This creates a dominant pole to ensure stability by moving the dominant pole to lower frequencies, introducing a zero (nulling resistor R1) to cancel the RHP zero. C2 (10pF) represents the load capacitance that the OTA must drive.

### Transistor Dimensions

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

## Results
We measured the performance of the proposed OTA using the parameters described in the following table

## OTA Performance Parameters

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
