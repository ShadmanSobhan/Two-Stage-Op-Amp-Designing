# 1-V, High-Gain, Wide-Bandwidth Two-Stage Op-Amp
In this repository, the basic theory, design, layout, and results of two stage differential Op-Amp are discussed.

## Design
The design of our proposed OTA is shown in the following figure.

The designed Operational Transconductance Amplifier (OTA) employs:

Current mirror biasing

Differential input pair with PMOS active load

Miller compensation for stability

600 µA bias current source

Low-voltage operation: 1 V±10%

Common-source output stage

The MOSFET devices used in the design, along with their sizing parameters, are listed below.

MOSFET Sizing
Name	Purpose	Length	Finger Width	Multiplier	Fingers
N1	Current Mirror	500 nm	5 µm	8	6
N2	Tail Current Source	500 nm	5 µm	12	6
N3	Gain Stage NMOS	500 nm	5 µm	52	6
N4	Input Differential Pair (−)	500 nm	5 µm	12	6
N5	Input Differential Pair (+)	500 nm	5 µm	12	6
P1	Active Load	500 nm	5 µm	12	6
P2	Active Load	500 nm	5 µm	12	6
P3	Gain Stage PMOS	250 nm	5 µm	100	6
