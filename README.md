# 1-V, High-Gain, Wide-Bandwidth Two-Stage Op-Amp
In this repository, the basic theory, design, layout, and results of two stage differential Op-Amp are discussed.

## Design
The design of our proposed OTA is shown in the following figure.

The OTA uses current mirror techniques, differential pairs with PMOS as the active load, Miller Compensation, a 600 \textmu A current source, a supply voltage of $1V \pm 10\%$, and a common-source output stage.

## Transistor Dimensions

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

