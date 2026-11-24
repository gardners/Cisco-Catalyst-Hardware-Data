# Cisco Catalyst Hardware Data

Independent measurement data, photographs, component identifications, reverse-engineered schematics, and **provisional** mechanical drawings of salvaged Cisco Catalyst switch hardware. This is an observation archive, not a replacement-board or product-design project.

## Find hardware data

Start with the findings linked below. Each assembly records the evidence and remaining measurements alongside its data.

| Assembly | Findings and reference files | Evidence / limits |
|---|---|---|
| [Catalyst 3560-X / 3750-X generation](catalyst-3560x/README.md) | Donor identification notes and module families | Exact donor model should be verified from its label; geometry is not guaranteed across variants. |
| [Mainboard mechanical survey](catalyst-3560x/mainboard/README.md) | **H01–H19 fitted hole centres**, measured edge planes, stepped perimeter, KiCad board template, SVG preview, and two **candidate** PSU connector locations | Hole coordinates are fitted relative measurements; board edge corners and PSU placement remain provisional. |
| [Front-panel LED/USB PCB](catalyst-3560x/front-panel/README.md) | [20-pin J2 map](catalyst-3560x/front-panel/docs/j2-pinout.md), [LED mapping](catalyst-3560x/front-panel/docs/led-driver.md), original circuit reconstruction, KiCad schematic and photos | Control-net continuity measured; logic supply not yet confirmed. |
| [715 W power supplies](catalyst-3560x/power-supplies/C3KX-PWR-715WAC/README.md) | [16-contact map and diagram](catalyst-3560x/power-supplies/C3KX-PWR-715WAC/pinout-research.md#all-sixteen-contacts), [enable connections](catalyst-3560x/power-supplies/C3KX-PWR-715WAC/pinout-research.md#enable-reports-and-the-unresolved-reference-contact), [standby findings](catalyst-3560x/power-supplies/C3KX-PWR-715WAC/pinout-research.md#standby-low-voltage-output-a-lead-not-an-established-rating), ratings and connector identification | External conversion evidence; six signal-function hypotheses and ten unknowns. Local pinout and exported standby rating unverified. |
| [C3KX-NM-10G network module](catalyst-3560x/network-modules/C3KX-NM-10G/README.md) | [Connector identification and sourcing](catalyst-3560x/network-modules/C3KX-NM-10G/connector/README.md), [192-contact photographic survey and probing resources](catalyst-3560x/network-modules/C3KX-NM-10G/connector/index-forensic-update.md), owner photos and port-mode matrix | TE signal-core identification documented; local contact index established. Electrical pin-to-net assignments unverified. |
| [BCM8727 component reference](components/BCM8727/README.md) | [Independent technical datasheet (PDF)](components/BCM8727/BCM8727_Open_Source_Datasheet.pdf), editable source and 324-position BGA register | Public-source chip reference; incomplete ball map. Cisco module routing documented separately. |
| [Fan cartridges](catalyst-3560x/fans/C3KX-FAN-23CFM/README.md) | Physical assembly and motor markings, connector investigation | Cartridge header pinout unverified. |
| [Connectors index](catalyst-3560x/connectors/README.md) | Known, candidate and unidentified connectors across assemblies | No candidate should be treated as a verified substitute. |
| [Chassis](catalyst-3560x/chassis/README.md) | Model envelope and observed shell, bays, bosses, front light-pipe features | Some dimensions are approximate, not registered to the hole survey. |

For a **PSU probing session**, use the [prioritised plan and blank measurement worksheets](catalyst-3560x/power-supplies/C3KX-PWR-715WAC/probe-plan.md). For the supporting research, use the [source review](catalyst-3560x/power-supplies/C3KX-PWR-715WAC/source-review.md) and [outstanding download queue](catalyst-3560x/power-supplies/C3KX-PWR-715WAC/download-queue.md).

## Measurement conventions

`MEASURED`: owner observations, meter results, caliper or ruler readings. `FITTED`: calculated from measured geometry; measurement assumptions apply. `VENDOR`: manufacturer's published specification. `CANDIDATE`: potential matching commodity part, not sample-verified. `INFERRED`: engineering interpretation or visual estimate. `UNVERIFIED`: awaiting tests.

**KiCad caution:** the motherboard `.kicad_pcb` is a geometrical survey/template, **not** a fabrication-ready board. H-series holes are centre marks, **not plated or drilled holes**. Edge.Cuts closes the provisional historical shape using some estimated transitions. The PSU connector overlay uses non-fabrication drawings only.

## Scope and provenance

All documentation concerns original Cisco components and their physical/electrical interfaces. Project-specific replacement circuits, proposed facias and subsystem plans are deliberately excluded. Manufacturer documents are linked rather than redistributed.

The original donor chassis was discussed as 3560-X/3750-X; PCB shapes and interface positions must not be assumed interchangeable between different chassis models or production revisions. These independently collected notes are not endorsed by Cisco or component manufacturers.

### Electrical safety

715 W PSUs accept mains power and can produce high-energy −56 V DC; unidentified contacts must not be energised on the basis of candidate pinouts. The front-panel supply could be 3.3 V or 5 V and has not been verified on a powered donor.

### Licence

Unless otherwise noted, the original content in this repository is licensed under the GNU Lesser General Public License, version 3 or (at your option) any later version (`LGPL-3.0-or-later`). See [LICENSE](LICENSE) for the licence notice, [COPYING.LESSER](COPYING.LESSER) for the LGPL terms, and [COPYING](COPYING) for the incorporated GPL version 3 terms.

Manufacturer trademarks and third-party copyrighted materials remain the property of their respective owners and are not relicensed by this notice.
