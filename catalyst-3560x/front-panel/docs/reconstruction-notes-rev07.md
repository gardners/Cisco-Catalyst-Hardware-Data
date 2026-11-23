# Cisco 3560-X front-panel PCB reverse engineering — Rev 0.7

**Cisco original PCB investigation | 23 November 2026 | unpowered meter investigation**

This revision supersedes the earlier description of **CR9 as a common-anode LED**. CR9 has **independent anodes** for its two dies; it is not legitimate to join pins 1 and 4 in the netlist. The drawing remains a reverse-engineering draft and must not be treated as a fabrication-ready board design. The pin-numbering convention is the user's assumption that CR packages have the same orientation as U2 and number anticlockwise.

## CR9: independently supplied yellow and green dies (meter-verified)

| CR9 physical pin | Measured connectivity | Function |
|---|---|---|
| 1 | To logic VDD **via 130-ohm resistor** (R25 association from user) | **Yellow anode** |
| 2 | To U1/1, SN74LV595A output | Yellow cathode |
| 3 | To U2/19, STP16CP05 output | Green cathode |
| 4 | **Direct to VDD, 0 ohms** | **Green anode** |

**Diode mode, unpowered:** red lead CR9/1, black CR9/2 = **yellow, 1.616 V**; red CR9/4, black CR9/3 = **green, 1.681 V**; reversed polarity = OL. These voltages were measured at meter test current, not normal LED current. Each pair is separate (1->2 and 4->3). The schematic uses a generic four-pin two-die LED model with independent anode pins and these connections explicitly assigned. Other LED colours/polarity pairings remain untested; do not generalise the CR9 colour map to all CRs without checking.

## Current-setting and 595 resistors

- **R6:** top marking **18B** (EIA-96: code 18 = 150, multiplier B = x10), **1.50 kohm**. Previous in-circuit reading ~875 ohm is superseded. Its path from U2/23 (R-EXT) to GND was inferred from the user's probe report and should be verified if required. Nominal STP16CP05 output current ~13 mA if R6 is indeed R-EXT; current is set by R-EXT, not by direct supply/series-resistor division.
- **R15:** **1 kohm** from U1 pin 10 (active-low /SRCLR) to **logic VDD**. The user followed the far end to the VDD fill. That fixes the floating-input concern and is connected correctly in the revised KiCad netlist.
- **R20, R21, R24, R25:** each **130 ohms**, user-meter measured. CR4/CR5/CR9/CR10 are the four LED packages with at least one 595 cathode output. CR9's pin 1 path through R25 is assigned in the schematic; **the remaining three physical ref-to-LED associations are unverified**, so their schematic references remain `R201`, `R202`, `R204` *placeholders*, with measured values set to 130R. Do not infer that every package anode is internally/common shorted: CR9 is explicitly split.
- **Supply voltage is NOT yet measured.** 3.3 V is favoured over 5 V because of the 595's recommended current; resistors and low-current diode readings do not establish VDD.

## J2 connector and serial chain

J2 numbering: pin 1 at top, pin 20 bottom of the supplied PCB photograph. Full measured and inferred pinout in `J2_pinout_measured.csv`.

| Pins | Function | Basis |
|---|---|---|
| 2, 5, 8, 16, 20 | GND | Meter continuity to chassis/ground plane |
| 3, 4 | USB D+, USB D- | J1/3 and J1/2 respectively, user probed |
| 6, 7 | USB VBUS | Both connect to J1/1, not necessarily logic VDD |
| 9, 10 | Common logic VDD | U1/16 and U2/24; **voltage unknown** |
| 1 | SW1 input | Unpopulated switch pad 1 to J2/1; pads 2,3 GND |
| 11 | Apparent terminal test pad | Not proven electrically unconnected |
| 12 | Serial chain readback | J2/12 visually traced to U1/9 QH-prime; meter check outstanding |
| 13 | Active-low output enable | U1/13, U2/21 |
| 14 | Serial data in | U2/2 SDI |
| 15 | Common shift clock | U2/3 and U1/11 |
| 17 | Common latch | U2/4 and U1/12 |
| 18 | Aux LED sink 0 | U2/5 via R23 (value ~200R unverified) |
| 19 | Aux LED sink 1 | U2/6 via R22 (value unmeasured) |

U2 pin 22 SDO is connected to U1 pin 14 SER. Thus a **single 24-bit serial chain** drives the LEDs. Data, clock, latch and /OE use four control signals; optional readback at J2/12 is one input; SW1 at J2/1 is another input. Latch behaviour and data bit order should be checked against the two manufacturer datasheets before coding controller logic.

## LED cathode outputs

All 20 LED cathodes have been mapped by the user: details in `LED_to_driver_measured.csv` and `LED_outputs_by_driver.csv`. CR9's cathodes and colours are confirmed; the rest of the colour map is not yet established. U1 pin 15 unused or test pad; U2 pin 20 no visible trace; these are not proven electrically NC.

## Remaining uncertainties / verification

- Actual logic VDD: **3.3 vs 5 V not proven**. Measure the original Cisco motherboard supply pin before energising the panel.
- Other three 130R resistor designators to CR4/5/10 require optional continuity checks; R25/CR9 association from user observation is recorded but PCB resistor-pad direct check not repeated.
- U2/23 -> R6 -> GND requires pin-to-pad verification if a production-grade schematic is desired; marking establishes resistance value.
- J2/12 -> U1/9 is visual trace reconstruction not zero-ohm meter verified; J2/11 appears a pad only.
- USB filter/protection passive components (FL1, etc.) are placeholders; pin-level USB data and VBUS connectivity are measured but topology remains incomplete.
- CR4, CR5, CR10 have two cathodes driven by 595, their two anode pins were observed to share the post-resistor supply; confirm individual packages if strict validation needed.

## Schematic status

The `.kicad_sch` includes embedded custom symbols, measured J2 nets, complete LED-to-driver cathode map, resistor networks and a generic four-pin *separate-anode* LED symbol. **In Rev 0.7, the CR9 pin 4 net is VDD directly, while CR9 pin 1 remains on the downstream side of the 130R resistor.** R15 now pulls /SRCLR to VDD; R6 is 1k5. Internal parse/net checks were run, but **KiCad GUI, ERC and physical-board checks were not available here**. No manufacturing footprint has been proved.

Datasheets: STP16CP05 https://www.st.com/resource/en/datasheet/stp16cp05.pdf and TI SN74LV595A https://www.ti.com/lit/ds/symlink/sn74lv595a.pdf
