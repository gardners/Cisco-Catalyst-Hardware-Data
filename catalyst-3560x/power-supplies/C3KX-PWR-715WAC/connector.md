# Candidate power-supply connector — not verified

Owner's observations of the Cisco PSU-to-motherboard contact assembly:

| Feature | Reported datum | Status |
|---|---:|---|
| Heavy electrical contacts | 2 | observed |
| Smaller control contacts | 16 | observed |
| Large guide feature centre spacing | ~30.0 mm | measured |
| Guide feature inner-edge gap | ~25.5 mm | measured |
| Original Cisco mainboard thickness | ~2.4 mm | measured |
| Connector mechanical interface | Flush with a local motherboard edge | observed |
| Two small connector board-lock positions | 31.75 mm apart | **candidate drawing-derived/photo-registered hypothesis**, NOT physically caliper-confirmed |
| Board-lock setback from local board edge | 6.35 mm | candidate drawing-derived/photo-registered hypothesis |
| Two PSU connector positions | ~91 mm apart | approximate photo-based offset, **not** direct centre-to-centre measurement |

Candidate: **Amphenol/FCI `51760-10101601AALF`**, a 1P + 16S + 1P right-angle receptacle. Amphenol lists the mate as **`51720-10101601AALF`**. Four signal rows on a nominal 2.54 mm pitch; two power contacts. The actual Cisco module and original motherboard component have not been positively matched to these SKUs.

Other previously investigated, lower-confidence alternatives: `51740-10101601AALF` (different orientation), `10106126-4004001LF`, `51770-030LF`, `51740-10201602AALF` (different guide/power-contact configurations; do not treat as matches).

## Position investigation

The first small board-lock feature of each candidate footprint was **estimated** at ~11 mm and ~102 mm from the original PCB's local left edge (pitch ~91 mm). The candidate footprint's second board-lock is 31.75 mm farther along X. The fitted mainboard survey places the relevant local left edge at underside X≈−13.13 mm and local mating edge at Y≈87.60 mm. Those hypotheses are translated into local survey coordinates in [`../../mainboard/psu-socket-hypotheses.csv`](../../mainboard/psu-socket-hypotheses.csv), which also documents the *unverified* placement assumptions. The KiCad drawing uses no manufactured connector pads/holes for them.

**Do not conclude** DC blade polarity, protective earth, control pin functions or contact sequence from the geometric match. Physical insertion/alignment and manufacturer's mechanical drawings must precede any PCB footprint release.

References: [Amphenol product](https://www.amphenol-cs.com/product/5176010101601aalf.html), [Cisco specifications](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3750x_3560x/hardware/installation/guide/3750x_3560x_HIG/HIGSPEC.html).
