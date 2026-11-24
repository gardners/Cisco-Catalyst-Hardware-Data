# Catalyst 3560-X / 3750-X generation: observed hardware

This collection documents a physically inspected 24-port PoE+ Cisco Catalyst donor, two C3KX-PWR-715WAC modules and the associated front LED/USB card. Discussions identified the chassis as a 3560-X or 3750-X at different stages. The case label was not definitively recorded; therefore do not treat the board outline as a universally confirmed 3560-X mechanical drawing.

- [Original Cisco mainboard survey](mainboard/README.md) — relative holes, edge measurements, PSU socket location hypotheses and KiCad geometry.
- [Front-panel daughterboard](front-panel/README.md) — [20-pin J2 map](front-panel/docs/j2-pinout.md), LED mapping and reconstructed electrical schematic.
- [Power supply modules](power-supplies/C3KX-PWR-715WAC/README.md) — [16-contact research map, enable and standby findings](power-supplies/C3KX-PWR-715WAC/pinout-research.md), [prioritised probe plan](power-supplies/C3KX-PWR-715WAC/probe-plan.md), factory ratings and candidate Amphenol connector.
- [Network modules](network-modules/README.md) — C3KX-NM-10G identification, photos, port modes, and [192-contact survey and probing resources](network-modules/C3KX-NM-10G/connector/index-forensic-update.md). The [BCM8727 component reference](../components/BCM8727/README.md) covers the PHY separately.
- [Fan cartridges](fans/C3KX-FAN-23CFM/README.md) — factory cooling cartridge and connector observations.
- [Chassis](chassis/README.md) — physical constraints, shell dimensions and future light-pipe survey.
- [Connector index](connectors/README.md) — confirmed and candidate parts, including uncharacterised proprietary contacts.

`3560-X`/`3750-X` share several Cisco spare-module families; interchangeability of entire boards, fan connectors, and mechanical mounting is **not** established by that fact alone.
