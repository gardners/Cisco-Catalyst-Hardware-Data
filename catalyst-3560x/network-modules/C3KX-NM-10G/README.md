# Cisco Catalyst C3KX-NM-10G hardware data

This is a **hardware-observation repository**, not a chip datasheet or a proposed replacement design. For the BCM8727 family, see the repository [independent open-source BCM8727 datasheet](../../../components/BCM8727/BCM8727_Open_Source_Datasheet.pdf), and original Broadcom/Terasic/Altera/Linux references collected under [references](references/references.md).

## Physical identification

| Property | Value | Confidence |
|---|---|---|
| Assembly | Cisco C3KX-NM-10G; SFP/SFP+ uplink module | Cisco published |
| Four cages | G1/G2 and G3/G4 (G2/G4 10G capable) | Cisco published |
| Module PCB P/N | `73-12299-04 B0` visible on owner photo | Photographically observed |
| Secondary board silkscreen | `28-9062-04` on underside | Photographically observed |
| PHY | Broadcom BCM8727-family device, centred on component side | Photographically observed |
| Host signal connector | TE Connectivity `1934225-1`, Z-PACK TinMan 192-position right-angle press-fit receptacle | Owner identified, TE product record |
| Signal mating connector | TE `1934318-1`, mechanically compatible header (TE-listed family mate); whether this is Cisco's actual fitted part is unconfirmed | TE product record; installed PCB variant not verified |
| Signal connector termination | Through-hole compliant press-fit; no reflow required for this component | TE published |
| Power contacts | Separate outer Tyco connector/guide overlay with eight visible side contacts; voltage, polarity and attachment method not measured | Owner photo/observation |
| Module-side power overlay marking | `1926944-1` (owner-observed; identification as a standalone orderable TE part unverified) | Reported, not supplier verified |
| Mainboard-side power overlay marking | `1926945-1` and `1126 STD` legible on user macro photo | Photographically observed |
| High-speed host protocol | BCM8727 supports two XAUI channels (four differential lanes each direction) | Broadcom published for chip; routing not measured on Cisco PCB |
| G1/G3 1GbE routing | Unknown | Open |
| Module input rails and power consumption | Unknown | Open |

## Photos (owner-supplied, 23 Nov 2026)

- [01 module underside](photos/01-module-underside.jpg) (original file PXL_20261123_174502605.jpg; solder-side connector footprint and AC coupling network).
- [02 module component side](photos/02-module-component-side.jpg) (original file PXL_20261123_174517852.jpg; BCM8727, regulators, SFP cage).
- [03 module connector mating face](photos/03-module-connector-mating-face.jpg) (original file PXL_20261123_174537871.MACRO_FOCUS.MP.jpg).
- [04 switch motherboard connector rear](photos/04-switch-mainboard-connector-solder-side.jpg) (original file PXL_20261123_174602375.MACRO_FOCUS.jpg).
- [05 switch motherboard connector marking](photos/05-switch-mainboard-connector-marking.jpg) (original file PXL_20261123_174634748.MACRO_FOCUS.jpg; `1926945-1`).

The separate third-party promotional image previously shown in conversation is **not** included here.

## Cisco slot and port matrix

Per pair (G1/G2, G3/G4), Cisco specifies either **two 1GbE SFPs** or **one 10GbE SFP+** in the corresponding 10G-capable cage. Four gigabit ports or two 10G ports are possible; G1/G3 cannot operate simultaneously with 10G in their paired cages. See [port matrix](measurements/port-mode-matrix.csv) and [Cisco notes](references/references.md).

## Data still needed

- Exact pin numbering and pin-to-net map of the 192-position signal section and eight side power contacts; installed Cisco header SKU remains unverified.
- Verify the motherboard assembly termination, including external power overlay. TE confirms press-fit for `1934225-1` and its TinMan connector family; this alone does not confirm every installed power blade is press-fit.
- Original module supply rails, ground contacts, reference-clock source, PHY reset and management signalling.
- G1/G3 1000BASE-X paths, G2/G4 mode changes and high-speed AC coupling details.
- Mechanical XY location of connector relative to the motherboard H01--H19 survey.

See [connector inventory](connector/README.md) and [measurements](measurements/README.md).
