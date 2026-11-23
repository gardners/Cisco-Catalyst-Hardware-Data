# J2 — 20-pin motherboard interface

**Numbering convention:** board viewed component-side-up, with the 20-pin
connector on the left, **pin 1 at the top, pin 20 at the bottom**. See
[annotated image](../photos/j2-pins-numbered.png). Verify orientation
before making a mating cable: these numbers refer to PCB contacts, not a
specified mating connector manufacturer's drawing.

| J2 contact | Recovered function | Unpowered resistance to GND | Basis |
|---:|---|---:|---|
| 1 | SW1 (to GND when pressed, expected) | open to GND | Meter |
| 2 | GND | ≈0 ohm | Meter |
| 3 | USB D+ | ≈885 ohm | Meter |
| 4 | USB D− | ≈885 ohm | Meter |
| 5 | GND | ≈0 ohm | Meter |
| 6 | USB VBUS | infinity | Meter |
| 7 | USB VBUS | infinity | Meter |
| 8 | GND | ≈0 ohm | Meter |
| 9 | Logic VDD (3.3/5 V unverified) | ≈727 ohm | Meter |
| 10 | Logic VDD (3.3/5 V unverified) | ≈727 ohm | Meter |
| 11 | Terminating test pad (apparently unused) | infinity | Visual only |
| 12 | Serial readback U1/QH′ (visual) | infinity | Visual only |
| 13 | Active-low output enable | ≈1753 ohm | Meter |
| 14 | Serial data to U2 | infinity | Meter |
| 15 | Shared clock | ≈873 ohm | Meter |
| 16 | GND | ≈0 ohm | Meter |
| 17 | Shared latch | ≈873 ohm | Meter |
| 18 | U2 OUT0 via R23 | ≈953 ohm | Meter |
| 19 | U2 OUT1 via R22 | ≈953 ohm | Meter |
| 20 | GND | ≈0 ohm | Meter |

The measured/visual source details are preserved verbatim in
[`j2-pinout.csv`](../measurements/j2-pinout.csv). Pin 11's function is
**not** verified as electrically open; it appears to end at a test pad.
J2/12 was followed visually under U2 to U1/9, rather than established
by end-to-end meter continuity.

## Original connector control signals

To control the LEDs, use four GPIO **outputs**: J2/14 (`DATA`), J2/15
(`CLOCK`), J2/17 (`LATCH`), J2/13 (`/OE`). J2/12 (serial chain out) and
J2/1 (SW1) are optional **inputs**. Do not assume signal-voltage compatibility
until the board logic rail is measured. No on-board SPI bus controller was
identified; these are low-level shift-register signals.

## USB caveat

J2/3 = J1/3 (D+), J2/4 = J1/2 (D−), J2/6 and J2/7 = J1/1
(VBUS), and J1/5 = ground. The protection/filter topology is not
fully mapped. It is a USB **connector only**: using it as a USB console
requires your own appropriate USB device controller or USB-to-UART bridge.
Do not tie USB VBUS directly to the logic-VDD net.
