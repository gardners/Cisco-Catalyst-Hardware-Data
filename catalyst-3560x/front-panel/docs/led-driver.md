# LED-driver serial chain and LED assignments

## Serial chain

```text
DATA (J2/14) → U2 STP16CP05 SDI (pin 2)
                      U2 SDO (pin 22) → U1 SN74LV595A SER (pin 14)
                      U1 QH′ (pin 9) → J2/12 (visual trace)

J2/15 CLOCK → U2 pin 3 + U1 pin 11
J2/17 LATCH → U2 pin 4 + U1 pin 12
J2/13 /OE   → U2 pin 21 + U1 pin 13
```

Thus there are **24 shifted bits** (16 on U2 and 8 on U1), although
just 20 LED cathodes are assigned. The exact bit pattern, latch timing,
polarity and any setup/hold requirements must be implemented using the
**manufacturer datasheets** rather than guessed from these signal names.
U1/10 (/SRCLR) has a 1 kΩ pull-up (R15) to logic VDD.

## Cathode continuity measurements

All 20 cathodes were mapped by meter; order is PCB reference-number order,
*not* necessarily front-panel physical order.

| LED package | Pin 2 cathode | Pin 3 cathode |
|---|---|---|
| CR1 | U2 pin 8 | U2 pin 7 |
| CR2 | U2 pin 9 | U2 pin 10 |
| CR3 | U2 pin 14 | U2 pin 13 |
| CR4 | U1 pin 3 | U1 pin 2 |
| CR5 | U1 pin 7 | U1 pin 6 |
| CR6 | U2 pin 12 | U2 pin 11 |
| CR7 | U2 pin 18 | U2 pin 17 |
| CR8 | U2 pin 16 | U2 pin 15 |
| CR9 | U1 pin 1 | U2 pin 19 |
| CR10 | U1 pin 5 | U1 pin 4 |

U2 outputs 5 and 6 (OUT0 and OUT1) also route, via R23 and R22,
to J2 pins 18 and 19 respectively. U2/20 (OUT15) has no obvious
surface track; U1/15 (QA) reaches a test point or blind via. Their
actual use is not electrically verified.

## LED anodes and resistors

- For the U2-only packages CR1/2/3/6/7/8, user continuity measurements
  indicate that anodes (pins 1 and 4) are at logic VDD.
- CR4/5/10 have both cathodes on U1 and their two anodes reportedly
  share a post-resistor node fed through **130 Ω** from VDD.
- **CR9 is different**: pins 1 and 4 are **not shorted**. Pin 1 (yellow)
  is fed from VDD through R25 = 130 Ω and goes with U1/1 on pin 2;
  pin 4 (green) goes **directly** to VDD and goes with U2/19 on pin 3.
- Physical resistors R20, R21, R24, R25 were measured as 130 Ω;
  **R25→CR9** is the provisional association from physical location;
  direct pad-to-pad resistor mapping was not separately recorded. The other
  three resistor-to-package mappings need a continuity check.

## CR9 diode test (unpowered Uptek LP-310)

| Anode (+ red) | Cathode (− black) | Observed | Reading |
|---:|---:|---|---:|
| CR9/1 | CR9/2 | Yellow | 1.616 V |
| CR9/4 | CR9/3 | Green | 1.681 V |

Both pairs read `OL` with probes reversed. These are multimeter-test-current
voltages, **not** the forward voltages at normal operating current. Do not
generalise CR9's die-colour mapping to all other CR packages without testing.

## Schematic fidelity

The KiCad drawing uses custom embedded symbols and is a reverse-engineered
**electrical representation**, not a manufacturing design. It contains
provisional resistor reference designators for unmatched resistors. It is
possible to drive a chain with shared control lines, but bit order and
electrical compatibility still require verification.
