# First PSU session — unpowered contact and return checks

This is the short starting session for **each OEM separately**. It resolves the four visible power contacts and follows up the [continuity-only M1 observation](measurements/2026-11-25-case-bond.md). No enable jumper, load resistor or mains-powered test is needed for this session. The later sequence is in [probe-plan.md](probe-plan.md).

## Set up the record

1. Copy [power-contact-checks-template.csv](power-contact-checks-template.csv) under a session-specific filename. Record the full Cisco/OEM label, suffix/revision, specimen ID, date and meter model. Confirm which module was used for M1 if known; otherwise retain M1's unknown specimen.
2. Disconnect the PSU from mains, the switch and all external wiring. Keep the enclosure closed; verify accessible DC contact voltages have decayed before selecting resistance mode.
3. Use the archive's module mating-face orientation: **fan right, broad metal wall above, folded seam below**. Take or annotate an owner photograph.
4. Give the **four individually accessible power contacts** temporary IDs `PC01`–`PC04` and mark their physical positions in that photo. These IDs deliberately have **no predefined positions, polarity or net grouping**. Record the mapping for each specimen; they are not Cisco/Amphenol pin numbers or four asserted rails.
5. Select **resistance mode**, record the reading with the probes shorted together, then separate them and note the meter's open-circuit indication. A continuity beep/no-beep result is a different observation; retain the actual displayed resistance or `OL`.

## Record the checks

The CSV has 22 checks per OEM, with all actual readings blank. Red/black probe placement is specified so polarity-sensitive paths can be compared.

| Order | Connections | Question resolved |
|---|---|---|
| 1 | Case to protective-earth inlet contact | What case bond does the meter show relative to its shorted-lead reading? |
| 2–5 | Each of PC01–PC04 to case | Is there a detectable DC path from any individual power contact to the case? |
| 6–11 | All six pairs among PC01–PC04 | Which contacts are candidates for the same output net? |
| 12 | S10 to S12 | Do the two reported control-return candidates appear directly related? |
| 13–17 | S10 to each power contact and case | Which output or case reference, if any, is associated with S10? |
| 18–22 | S12 to each power contact and case | Does S12 share S10's reference or show a different path? |

For S10/S12 use the [signal map](pinout-research.md#physical-reference-and-numbering), not the temporary power-contact labels. Record readings that settle, drift or change range. Repeat ambiguous readings with reversed meter polarity and retain both results; do not substitute a beep for a resistance value.

## What the results would establish

- **Case close to the shorted-lead resistance:** supports a direct protective-earth bond under the measurement conditions.
- **No beep alone:** does not give a resistance value or establish isolation.
- **High resistance or `OL` to case:** supports no direct DC bond detected in that unpowered, disconnected state; it does not establish an output-to-earth working-voltage or insulation rating.
- **A contact pair consistently close to the lead resistance:** supports investigating a common net. Record polarity and settling behaviour before equating contacts; internal circuitry can also provide a low-resistance path.
- **Different S10/S12 relationships:** preserve them separately. Neither return should be tied to case or the chosen system ground just to make the readings agree.

Leave the original templates blank. Save the filled copy and labelled owner photo. **This is a useful stopping point:** it gives us a per-specimen contact grouping and return-path evidence to review before the AC-only voltage survey. It does not establish blade polarity or an external standby output by itself.
