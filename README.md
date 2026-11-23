# Cisco Catalyst Hardware Data

Independent measurement data, photographs, component identifications, reverse-engineered schematics, and **provisional** mechanical drawings of salvaged Cisco Catalyst switch hardware. This is an observation archive, not a replacement-board or product-design project.

## Catalogue

| Assembly | Data available | Confidence / open questions |
|---|---|---|
| [Catalyst 3560-X / 3750-X generation](catalyst-3560x/README.md) | Donor identification notes and module families | Exact donor model should be verified from its label; geometry is not guaranteed across variants. |
| [Mainboard mechanical survey](catalyst-3560x/mainboard/README.md) | **H01–H19 fitted hole centres**, measured edge planes, stepped perimeter, KiCad board template, SVG preview, and two **candidate** PSU connector locations | Hole coordinates are fitted relative measurements; board edge corners and PSU placement remain provisional. |
| [Front-panel LED/USB PCB](catalyst-3560x/front-panel/README.md) | Original circuit reconstruction, 20-pin J2 map, LED mapping, KiCad schematic, photos | Control-net continuity measured; logic supply not yet confirmed. |
| [Power supplies](catalyst-3560x/power-supplies/C3KX-PWR-715WAC/README.md) | Cisco 715 W module ratings, Delta/Lite-On identifiers, PwrBlade candidate connector | PSU 16-contact pinout, DC blade polarity, mating footprint unverified. |
| [Fan cartridges](catalyst-3560x/fans/C3KX-FAN-23CFM/README.md) | Physical assembly and motor markings, connector investigation | Cartridge header pinout unverified. |
| [Connectors index](catalyst-3560x/connectors/README.md) | Known, candidate and unidentified connectors across assemblies | No candidate should be treated as a verified substitute. |
| [Chassis](catalyst-3560x/chassis/README.md) | Model envelope and observed shell, bays, bosses, front light-pipe features | Some dimensions are approximate, not registered to the hole survey. |

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
