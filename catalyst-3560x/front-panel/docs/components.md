# Components and electrical notes

| Ref. | Identification | Role | Evidence |
|---|---|---|---|
| U1 | TI SN74LV595A | 8-bit serial shift register with CMOS outputs | IC marking and pin tracing |
| U2 | ST STP16CP05 | 16-output constant-current LED sink, serial interface | IC marking and pin tracing |
| J1 | Mini-USB type B | Physical USB connector to mainboard | Connector and continuity |
| J2 | 20-contact SMD header | Mainboard power, USB and LED signals | Direct tracing/meter |
| SW1 | Unpopulated four-pad switch | Active-low switch input via J2/1 | Pad continuity |
| CR1–CR10 | Four-terminal two-colour LED packages | 20 LED dies | Continuity; CR9 diode mode |
| R6 | `18B` EIA-96 code = 1.50 kΩ | Probable U2 R-EXT resistor | Marking; U2/23 connection still merits direct confirmation |
| R15 | 1 kΩ | U1/10 pull-up to VDD | Meter |
| R20/R21/R24/R25 | 130 Ω each | U1-driven LED current limit | Meter; R25 tentatively associated with CR9 |
| R22 | Value not measured | U2/6 → J2/19 | Trace/meter |
| R23 | ≈200 Ω **unverified** | U2/5 → J2/18 | Tentative in-circuit reading |
| FL1, Z1, etc. | Not fully identified | USB filtering / protection | Photographic inspection only |

## Supply voltage and current limits

The PCB's **logic VDD at J2/9 and J2/10 has not been measured**.
U1/16 and U2/24 connect to this net. J2/6 and J2/7 instead carry USB
VBUS from J1/1. Do not merge them.

If R6 really connects U2 pin 23 (R-EXT) to GND, its 1.50 kΩ value
suggests a nominal constant-current sink setting around **13 mA**.
That is an estimate, not a direct current measurement.

A U1-driven LED has an approximately 130 Ω anode feed. Its current is
approximately `(VDD − VF − VOL) / 130 Ω`. At an illustrative operating
forward voltage of 2.0–2.2 V and U1 low output of 0.3 V:

| Assumed logic VDD | Estimated U1 LED current |
|---|---|
| 3.3 V | 6.2–7.7 mA |
| 5.0 V | 19.2–20.8 mA |

These estimates favour 3.3 V on U1's recommended-output-current grounds,
**but are not proof**. CR9's meter-mode VF values (1.616/1.681 V) were
at much lower current and cannot be substituted for operating-current VF.
Measure the original motherboard supply (or establish reliable power-rail
evidence) before energising this panel.

## Datasheets

- [ST STP16CP05](https://www.st.com/resource/en/datasheet/stp16cp05.pdf)
- [TI SN74LV595A](https://www.ti.com/lit/ds/symlink/sn74lv595a.pdf)

**Status of KiCad file:** source from reconstruction revision 0.7; embedded
custom symbols; original footprint/mating connector not established;
KiCad graphical rendering and ERC are not yet verified. The schematic
should not be mistaken for a Cisco-published drawing.
