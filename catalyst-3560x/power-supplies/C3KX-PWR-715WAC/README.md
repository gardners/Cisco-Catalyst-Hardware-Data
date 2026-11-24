# Cisco C3KX-PWR-715WAC factory power-supply module

## Start here

| Looking for | Resource |
|---|---|
| Connector orientation and all 16 signal positions | [Contact map and evidence table](pinout-research.md#all-sixteen-contacts), [original diagram](figures/signal-contact-map.svg), [CSV worksheet](connector-pinout-worksheet.csv) |
| Main-output enable and power-blade polarity | [Reported enable connections](pinout-research.md#enable-reports-and-the-unresolved-reference-contact) and [output reference](pinout-research.md#power-contacts-and-the-sign-of-the-output) |
| Local case/earth and blade continuity observations | [M1: preliminary owner observations, 2026-11-25](measurements/2026-11-25-case-bond.md) |
| Low-voltage standby output | [Current findings and remaining uncertainty](pinout-research.md#standby-low-voltage-output-a-lead-not-an-established-rating) |
| What to measure next | [Prioritised probe plan](probe-plan.md), [connector readings](probe-readings-template.csv), [light-load readings](standby-load-tests-template.csv) |
| Sources and outstanding research | [Source review](source-review.md) and [download queue](download-queue.md) |
| Connector part and mechanical fit | [Candidate connector investigation](connector.md) |

The contact map contains external evidence and working hypotheses; no electrical assignment has been verified on the local specimens.

## Inspected labels

- Cisco designation: `C3-KX-PWR-715WAC V01` (observed label), Cisco accessory family `C3KX-PWR-715WAC`.
- Lite-On OEM: **`PA-1711-1-LF REV:04`**.
- Delta OEM: **`EDPS-715AB`**.

## Published ratings, not verified electrical measurements

| Property | Cisco rating |
|---|---|
| Maximum power | 715 W |
| DC output | **−56 V / 12.8 A** |
| AC input | 100–240 V AC; 50/60 Hz |
| Enclosure dimensions (H×D×W) | ~35 × 260 × 83 mm |

Cisco publishes the voltage as **−56 V**. External conversion reports suggest blade polarity and enable contacts. On one specimen, the owner reports a **protective-earth-to-case bond and no continuity beep from case to any of four visible blade pins**. This was beeper-mode testing: no actual resistance or `OL` values were obtained, and the tested OEM is not yet identified; see [M1](measurements/2026-11-25-case-bond.md). A floating output remains a hypothesis. Both specimens still need resistance measurements; blade polarity, control/standby references, available auxiliary power and enable conditions remain unverified locally.

## Factory output connector

Observed interface: **two substantial DC blade contacts plus sixteen smaller control/signal contacts**. Guide feature centres were measured approximately 30 mm apart (~25.5 mm inside-edge gap). An Amphenol PwrBlade 1P+16S+1P part resembles this interface. This is a **candidate**, not a verified manufacturer identification or interchangeable part; see [connector investigation](connector.md).

The factory motherboard is ~2.4 mm thick at the interface. Its sockets appear flush with the PCB edge near holes H07/H08; see the **provisional and explicitly marked socket overlay** in [mainboard survey](../../mainboard/README.md).

The [signal-contact research and map](pinout-research.md) defines all 16 contact positions and records external evidence. Two Delta 715 W conversions show **S11–S12** joined; a related Lite-On **1100 W** report uses **S11–S10** and suggests sense and I²C contacts. A Delta repair owner labels both S10 and S12 as logic grounds, leaving S12's proposed sense role unresolved across variants. Six positions have working functional hypotheses; ten remain unidentified. These are **not locally verified assignments**. The [pin investigation worksheet](connector-pinout-worksheet.csv) includes source coordinates and the related 1100 W unit's published idle-voltage readings.

## Next probing session

The [prioritised probing plan](probe-plan.md) starts with unpowered return-path measurements, then checks S04/S15/S03 as possible standby-output contacts using light loads. It includes blank [connector-reading](probe-readings-template.csv) and [load-test](standby-load-tests-template.csv) templates. The reported 12/5/3.3 V, 0.5–1.5 A auxiliary supply remains unverified; voltage readings alone do not establish an available power output.

A repair report describes **internal 12 V standby and approximately 3 V logic**, but provides no external standby pin or current rating. The [source review](source-review.md) separates primary observations from proposals and reposts. The [download queue](download-queue.md) lists useful material that normal web access could not retrieve completely; downloaded third-party material belongs outside this repository.

## Source documents

- [Cisco technical specifications](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3750x_3560x/hardware/installation/guide/3750x_3560x_HIG/HIGSPEC.html)
- [Cisco power module service guide](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3750x_3560x/hardware/install/notes/pwr_note.html)
- [Amphenol PwrBlade 51760-10101601AALF candidate](https://www.amphenol-cs.com/product/5176010101601aalf.html)

**Warning:** This AC module contains hazardous mains circuitry and stores energy. The differing reported enable-reference contacts must be resolved on each specimen before treating either conversion report as a local standalone procedure.
