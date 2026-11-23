# Outstanding verification work

Please update the measured CSV tables and schematic together as evidence
improves. Prioritised items:

| Priority | Open check | Why it matters |
|---|---|---|
| High | Measure the **original Cisco VDD** on J2/9, J2/10 | Establish 3.3 V versus 5 V before powering or connecting external logic |
| High | Run the reconstructed `.kicad_sch` through KiCad GUI and ERC | File has been parsed/inspected, not verified by KiCad itself |
| Medium | Meter J2/12 ↔ U1 pin 9 (QH′) | Currently a visual copper-trace reconstruction |
| Medium | Verify U2/23 ↔ R6 ↔ ground | Confirms 1.5 kΩ really is the LED-current setting resistor |
| Medium | Follow physical R20, R21, R24 to CR4, CR5, CR10; verify R25→CR9 directly | Match all part references rather than using provisional schematic IDs |
| Medium | Check J2/11 test pad, U1/15 and U2/20 | Confirm whether contacts/driver outputs are truly unused |
| Medium | Measure R22 and R23 separately from the circuit | Confirm auxiliary output resistors and their intended purpose |
| Medium | Identify Z1, FL1 and full J1 USB protection/filter topology | Improve accuracy of USB path and cable/interface design |
| Medium | Verify LED colours and anode pairing for all CR positions | Only CR9's yellow/green pairing was actually diode-tested |
| Later | Establish mating connector and actual board assembly number | Needed for repeatable hardware reuse/mechanical design |
| Later | Confirm 24-bit serial shift ordering / latch behaviour on powered unit | Needed for robust serial-shift driver |

No test should assume a circuit's rated operating voltage based only
on the LED resistor values. Use controlled bench power and electrical
safeguards if a standalone power-up is eventually attempted.
