# PSU signal-contact map and external research

Research checked **2026-11-24**. This is a partial electrical identification of the original interface. **None of the assignments has been measured on the repository's Lite-On 715 W or Delta 715 W specimens.**

The strongest exact-family results are a Delta `EDPS-715AB A` / `C3KX-PWR-715WAC V02` bench-supply build [R1] and a separate Delta conversion video [R3]. Both show contacts **11 and 12** joined. A related Lite-On **1100 W** report enables the corresponding contact 11 by connecting it to **10**, and supplies tentative sense and I²C assignments [R2]. A Delta repair report adds useful ground annotations and an internal standby-voltage observation [R7]. None establishes a complete 715 W pinout.

The [source review](source-review.md) records corroboration, conflicting claims and rejected transfers. Material still requiring retrieval is prioritised in the [download queue](download-queue.md).

## Physical reference and numbering

Look **into the DC connector on the PSU module**, with the **fan to the right**, the broad sheet-metal wall above the connector, and the folded housing seam below it. This is the module mating face, not a motherboard socket or solder-side view. The source module photographs use this orientation [R1, R2]. A mating socket viewed from its own mating face is mirrored.

`S01`–`S16` are this archive's contact identifiers, now assigned left-to-right across each row, starting at the top. The old worksheet did not define their physical positions. They are **not asserted to be Amphenol or Cisco pin numbers**. The `D1`–`A4` coordinates below follow the diagram in Adam Lawrence's answer [R2]; its letters run bottom-to-top. The numeric positions coincide with the row-major numbers in Petrakis's diagram [R1].

```text
                       Broad sheet-metal wall

 Left power       S01/D1  S02/D2  S03/D3  S04/D4       Right power
 contact          S05/C1  S06/C2  S07/C3  S08/C4       contact       FAN
                  S09/B1  S10/B2  S11/B3  S12/B4                      -->
                  S13/A1  S14/A2  S15/A3  S16/A4

                       Folded housing seam
```

An [original SVG reference drawing](figures/signal-contact-map.svg) shows the same contact identities. It is schematic, not a footprint or a dimensioned connector drawing.

## All sixteen contacts

The voltage column contains **external measurements from Maarten's Lite-On C3KX-PWR-1100WAC V02**, with AC applied but the main output not enabled, relative to the **left power contact** [R2]. They are comparison data, not readings from a 715 W module. A reported zero is a voltage observation, **not proof of a ground connection or an unused pin**.

| Archive ID | R2 coordinate | R2 idle voltage (V) | Working identification for investigation | Evidence and limit |
|---|---|---:|---|---|
| S01 | D1 | 0 | Unknown | Voltage only [R2]. |
| S02 | D2 | 0.133 | Unknown | Low nonzero voltage; no supported function [R2]. |
| S03 | D3 | 3.25 | Unknown | Voltage only; not established as a standby supply [R2]. |
| S04 | D4 | 3.28 | Unknown | Voltage only; not established as a standby supply [R2]. |
| S05 | C1 | 0 | Unknown | Voltage only [R2]. |
| S06 | C2 | 0 | Unknown | Voltage only [R2]. |
| S07 | C3 | 0 | Unknown; short contact in external photographs | Marked short in the Lite-On report and Delta repair photograph; no demonstrated presence/inhibit function [R2, R7]. |
| S08 | C4 | 0 | High-side remote-sense candidate | Answer proposes a connection to left power contact P1 if remote sense is needed [R2]; not separately demonstrated on 715 W. |
| S09 | B1 | 3.28 | I²C clock candidate | Answer explicitly presents this as tentative [R2]; no bus capture. |
| S10 | B2 | 0 | Enable-reference / logic-return candidate | R2 reports B3–B2 startup on 1100 W. Delta repair owner marks this position as logic ground; measurement method unspecified [R7]. |
| S11 | B3 | 3.25 | Main-output enable candidate | Used in both reported enable arrangements [R1–R3]; R7 marks the short contact at about 3 V. Active-low interpretation remains an inference. |
| S12 | B4 | 0 | Delta turn-on endpoint / return candidate; conflicting sense hypothesis | Delta conversions join S11–S12 [R1, R3]; repair owner labels S12 logic ground [R7]. R2 instead proposes low-side sense to right blade P2. Do not merge these roles across variants. |
| S13 | A1 | 0 | Unknown | Voltage only [R2]. |
| S14 | A2 | 3.28 | I²C data candidate | Answer explicitly presents this as tentative [R2]; no bus capture. |
| S15 | A3 | 3.26 | Unknown | Voltage only [R2]. |
| S16 | A4 | 0 | Unknown | Voltage only [R2]. |

The [CSV worksheet](connector-pinout-worksheet.csv) carries the same positions, external reference voltages and source IDs. `INFERRED` there means an assignment carried across from external evidence, **not local verification**. Ten signal contacts still have no identified function. In particular, no pin has yet been identified reliably as standby power, power-good, AC-fail, current-share, fan control, fan tachometer, an address strap or a hot-swap interlock.

## Standby low-voltage output: a lead, not an established rating

The owner has encountered claims of a **12 V, 5 V or 3.3 V auxiliary output at roughly 0.5–1.5 A**, but a traceable source for those current ratings has not been located. No manufacturer rating or load-tested first-hand report establishing an **exported** auxiliary output on EDPS-715AB or PA-1711-1-LF was found.

There is now a specific first-hand **internal standby** lead: Adjal's Delta `EDPS-715AB B` repair report says the main converter would not start while **12 V standby and approximately 3 V logic** remained operating [R7]. The report does not identify a 12 V connector contact, return or available current. Its annotated photograph identifies approximately 3 V at S11 and labels S10/S12 as logic grounds. This strengthens the case for an internal auxiliary circuit, while leaving external availability unresolved.

R2's main-disabled 1100 W measurements show approximately 3.3 V on S03, S04, S09, S11, S14 and S15. The unassigned **S04 (3.28 V), S15 (3.26 V) and S03 (3.25 V)** are the initial standby-investigation shortlist. That prioritisation is an inference; they remain `UNKNOWN` in the map. S09/S14 are tentative bus pins and S11 is the enable candidate, so they are excluded from the first supply-loading pass. R2's discussion proposes that a standby output may exist, but does not demonstrate a particular pin's current capability. Its table does not show an external 5 V or 12 V rail in the measured state.

An internal auxiliary supply, an exported standby power rail, and a signal pulled up to that rail are different things. A high-impedance voltage reading cannot distinguish them. A pin that holds 3.3 V at a tiny load is still not proven capable of supplying an ampere.

The [prioritised probing plan](probe-plan.md) starts with the reference connections and the three unassigned high contacts, then uses light resistor loads to characterise them. It includes [connector readings](probe-readings-template.csv) and [load-test](standby-load-tests-template.csv) templates. Substantial loads and enable links are deferred until the contact's role and reference are corroborated. The source voltage reference is the **left blade**; logic return must not be assumed to mean the lower-potential main-output blade.

## Enable reports and the unresolved reference contact

| Report | Actual module identified by source | Reported connection in this archive's coordinates | What it establishes |
|---|---|---|---|
| Petrakis [R1] | Delta EDPS-715AB A; label photograph shows C3KX-PWR-715WAC V02 | S11–S12 (source's 11–12) | Author reports standalone operation of a 715 W unit. It does not identify each endpoint's circuitry. |
| FanPhys [R3] | Delta EDPS-715AB; description identifies C3KX-PWR-715WAC V02; suffix not established | S11–S12 | Sampled video frames at 202–212 s show the bridge and its highlighted position. Author reports use with RD6018; no connector standby measurement is shown in the sampled frames. |
| Maarten / Adam Lawrence [R2] | Lite-On C3KX-PWR-1100WAC V02 | S11–S10 (source's B3–B2) | Questioner confirms successful startup after the answer. The comment does not say whether the optional sense connections were also required. |

R2 additionally suggests S08 to the left power contact and S12 to the right power contact if remote sense is necessary. It does **not** demonstrate that these links are needed on either local 715 W specimen. R1's photographed fan is on the right, agreeing with the physical reference above; the correspondence between its drawn grid and the photograph remains an interpretation, not a sample measurement.

R7's owner-labelled grounds at both S10 and S12 offer a possible explanation for the Delta pair, but do not prove those contacts are directly joined. R2's proposed low-side sense is another possibility for its related model. These observations cannot establish whether there is a variant difference, an intervening network or an incorrect tentative assignment. **Do not short S10 and S12 together to resolve the uncertainty.**

The repair owner still could not start the main output after the suggested connection [R7]. The thread provides neither a successful repair nor proof of a minimum-load requirement. Its reply's jumper screenshots come from R3, so they are not another independent conversion experiment.

R1 also reports that the internal fan initially runs fast and slows after about a minute. That does not establish an externally accessible fan-control pin.

## Power contacts and the sign of the output

The archive's existing `POWER_BLADE_A` is now the **left** power-contact assembly in the view above; `POWER_BLADE_B` is the **right**. Each assembly has multiple visible mating surfaces; those are not additional independently identified rails.

Petrakis labels the left contact `56V` and the right `GND` [R1]. Lawrence calls them output high side P1 and low side P2 [R2]. R3 shows red wiring on the left and black on the right, consistent with that assignment, although wire colour is not a voltage measurement. Together these support **left = higher potential, right = lower potential** as an external candidate assignment, still unmeasured here.

Cisco specifies the module output as **−56 V at 12.8 A** [R4]. A 56 V differential can be expressed as left = +56 V relative to right, or right = −56 V relative to left. Neither convention establishes a connection to chassis or protective earth. In particular, the `GND` label in a conversion diagram is not evidence of an earth bond.

**Local observation added 2026-11-25:** on one specimen, the owner reports a **protective-earth-to-case bond** and **no continuity beep from case to any of four visible blade pins**. The owner clarified that only beeper mode was used: neither resistance values nor `OL` were measured. The tested OEM is not identified, and both specimens still need resistance checks; see [measurement M1](measurements/2026-11-25-case-bond.md). No beep does not establish a floating output or a permissible output-to-earth voltage. The four visible pins have not been electrically grouped by this observation. No polarity or control-return assignment is promoted to `MEASURED` from it.

## Measurements that will resolve the remaining pins

For a step-by-step session, use the [prioritised probing plan](probe-plan.md); the following is an overview.

1. Record each local module's complete Cisco PID/VID, OEM model, suffix and revision, and take an owner photograph in the reference orientation. Check whether S07 and S11 are the short contacts on each specimen. Keep Delta and Lite-On records separate.
2. With AC disconnected and the module discharged, measure resistance from every signal contact to each power contact and to the metal case, recording meter polarity and settling behaviour. Establish which contacts are actual returns before using the enable hypotheses. Check S08 and S12 against their proposed power rails; distinguish a sense-network resistance from a direct return.
3. Once the electrical reference is established, collect a per-pin voltage table for each 715 W module in the original switch's standby and running states. Record the voltage across both power contacts and each contact's relationship to the case independently.
4. With the logic reference and signal levels established, a passive capture while the original switch controls the supply can test S09/S14 for I²C and identify status transitions, fan-related signals and the two short contacts. An idle voltage alone does not identify a protocol or an output's current capability.
5. Promote individual assignments to `MEASURED` only with the module identity, orientation, reference and observation recorded. Resolve the S10/S12 difference before documenting a local standalone enable procedure.

## Sources and what was actually inspected

All links were checked on 2026-11-24. Only original prose, factual observations and the archive's own drawing are stored here. Third-party photographs, diagrams, article text, models and downloaded API responses are **not redistributed**.

- **R1 — Petrakis, [Dual channel bench power supply](https://makerworld.com/en/models/2610396-dual-channel-bench-power-supply)**, published 2026-04-03. Primary description retrieved through the [public model metadata endpoint](https://makerworld.com/api/v1/design-service/design/2610396); module/connector photographs and the embedded turn-on diagram were inspected. Direct [turn-on diagram](https://makerworld.bblmw.com/makerworld/model/DSM00000002610396/design/0620fc4b1ece83c6.png), [module label photograph](https://makerworld.bblmw.com/makerworld/model/DSM00000002610396/design/377372d72cf8093f.jpg) and [connector photograph](https://makerworld.bblmw.com/makerworld/model/DSM00000002610396/design/00a91949e4265e1f.png). The [3D GO index](https://3dgo.app/models/makerworld/2610396) helped locate the primary source; it is not an independent confirmation. No source assets copied into this repository.
- **R2 — Maarten and Adam Lawrence, ['Jump starting' Lite-eon Server Power Supply](https://electronics.stackexchange.com/questions/476293/jump-starting-lite-eon-server-power-supply)**, question 2020-01-15, useful answer 2020-01-17. First-hand questioner's measurements and success comment; answer's pin roles are proposals based on experience with other Cisco supplies. Inspected [voltage photograph](https://i.sstatic.net/1XwwL.jpg), [short-contact photograph](https://i.sstatic.net/sX05o.jpg) and [coordinate diagram](https://i.sstatic.net/2gDJn.png). The subject is 1100 W, not PA-1711-1-LF. No source assets copied.
- **R3 — FanPhys, [Cheap 715W 56V PSU for Hobby Electronics: Delta EDPS-715AB](https://www.youtube.com/watch?v=h07NQ-fHocA)**, 2023-12-12. Description and all 151 available storyboard frames, sampled every two seconds across approximately five minutes, inspected. [Connector close-up begins around 202 s](https://www.youtube.com/watch?v=h07NQ-fHocA&t=202); the overlay at 208–212 s highlights S11–S12. This is independent visual evidence of the conversion connection. Audio, full-motion video, transcript and comments were not retrieved; the caption request returned an empty response. No source frames stored here.
- **R4 — Cisco, [Installation Notes for Catalyst 3750-X and 3560-X Switch Power Supply Modules](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3750x_3560x/hardware/install/notes/pwr_note.html)**, April 2010 / revised April 2013; [PDF](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3750x_3560x/hardware/install/notes/pwr_note.pdf), Table 7, printed page 17. Manufacturer source for −56 V / 12.8 A; no internal 16-contact pinout. Table 5 distinguishes input-present, output-disabled and output-failed LED states.
- **R5 — Cisco, [Power Supply and Fan Module Installation](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3750x_3560x/hardware/installation/guide/3750x_3560x_HIG/HIGFRU.html)**, Table 3-1 and its footnote. Says the listed PWR-C1 replacements are functionally compatible with C3KX-PWR supplies and have an extended protective tab. This is family context, not confirmation of individual pin roles or of every later platinum variant.
- **R6 — oreo, [Good money after bad — Solar upgrade time, page 2](https://www.thebackshed.com/forum/ViewTopic_mobile.php?P=2&TID=16960)**, posts dated 2025-01-10. First-hand C3KX-PWR-715WAC reuse in battery/bench setups, but no usable 16-contact assignment in the inspected posts. No grounding modifications from other PSU models in that thread are adopted here.
- **R7 — Adjal / Asket, [Delta EDPS-715AB B repair discussion](https://forum-monitor.net.ru/threads/693087/)**, three public posts dated 2026-05-12, in Russian. Original owner reports and [annotated connector photograph](https://forum-monitor.net.ru/attachments/260738/) inspected, along with the public internal photograph and reply screenshots. Ground labels and internal standby voltages are owner reports, not local measurements. The reply screenshots reproduce R3; no successful repair is documented. No source assets copied.

Two other leads did not supply pin evidence: the [esk8 conversion discussion](https://forum.esk8.news/t/charger-from-server-power-supply/40869) is mainly a charger suitability discussion; the [RCGroups post linked from R2](https://www.rcgroups.com/forums/showpost.php?p=40032474&postcount=4091) describes a Dell L1100A-S0 / Lite-On PS-2212 12 V supply with a different connector. Its numbered pins are not transferable to this module.
