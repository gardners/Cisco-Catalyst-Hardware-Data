# Cisco C3KX-NM-10G signal and power connector assembly

## Identified signal connector

| Feature | Finding | Evidence |
|---|---|---|
| Sled signal section | **TE Connectivity 1934225-1**, Z-PACK TinMan | Owner component identification; TE product page [TE-1934225] |
| Configuration | 192 contacts; 12 rows x 16 columns, right-angle receptacle | [TE-1934225] |
| Signal PCB termination | Through-hole **press-fit**, with compliant eye-of-needle contacts; not SMT/reflow | [TE-1934225], [TE-114-13202] |
| Mating signal header | **TE 1934318-1**, 192-position vertical header (compatible mate specified by TE); **not yet confirmed as the actual fitted Cisco half** | [TE-1934318], [TE-TinMan-catalog] |
| Mating-face power contacts | Eight larger contacts (four per side) in a **separate external housing/overlay** | Owner photographs; electrical roles unknown |
| Module-side overlay moulding | `1926944-1` | Owner-reported; independent part listing unconfirmed |
| Motherboard-side overlay moulding | `1926945-1`, smaller `1126 STD` | Owner macro photograph |
| Outer overlay vendor | Tyco Electronics visible on module-side overlay | Owner observation; independent OEM ordering number not verified |

The module connector is a **mixed signal/power assembly**, not a single monolithic 200-pin TE 1934225-1 part. Treat 1934225-1 as the **192-contact signal core**, and 1926944-1 / 1926945-1 as observed markings on the external power/guide assemblies. The outer units' relationship to any currently orderable part number, their termination method, and their rated power contacts remain **unconfirmed**.

## Press-fit extraction and reuse

The TE Z-PACK TinMan application specification **114-13202** explicitly describes compliant press-fit headers and receptacles, suitable for unsoldered production installation. This makes **mechanical extraction plausible**, but it is not a promise of straightforward or electrically qualified reuse. The specified installation requires board support and proper seating tools; extraction of a 192-contact assembly requires evenly applied force and the corresponding backing fixtures. **Do not pry against the Cisco multilayer PCB or pull on the housing without a removal fixture.**

* The 192-signal press-fit connector might be removed mechanically from the donor board if all associated constraints permit it.
* The external Tyco power-blade overlay may constrain removal and may have a different attachment method. Inspect it separately.
* Individual header pins have a repair procedure (TE tool 1976935-1); **the receptacle does not support individual contact replacement** according to the application specification.
* Prior press-fit contacts and plated-through holes can suffer mechanical damage. An extracted connector is **unqualified for production reuse** unless separately assessed and tested; purchase a new connector when available.
* The connector's final installed orientation, board stack-up and datum must be taken from the relevant TE customer drawing, not assumed from photographs.

## Open measurements

- Determine whether the installed Cisco motherboard-side signal header is TE 1934318-1 or a Cisco-specific variant.
- Identify actual signal-corner pin index and module-side pin numbering using manufacturer product drawing.
- Extract module power pins (GND, power rails, presence, reset, clock, management) using non-powered continuity testing, recording resistances.
- Determine whether `1926944-1` and `1926945-1` are standalone part numbers or markings of the overmoulded guides/power units.
- Confirm motherboard connector location against the H01-H19 mounting-hole survey.

## Primary part and tooling references

[TE-1934225]: https://www.te.com/en/product-1934225-1.html
[TE-1934318]: https://www.te.com/en/product-1934318-1.html
[TE-114-13202]: https://www.farnell.com/datasheets/1922330.pdf
[TE-TinMan-catalog]: https://www.te.com/en/product-1934225-1.html

Product drawing and specification links are available directly on the two TE product pages. The standalone document URLs above may move; prefer the product-page document lists.

## Photographs

- [Module mating face](../photos/03-module-connector-mating-face.jpg)
- [Mainboard contact field](../photos/04-switch-mainboard-connector-solder-side.jpg)
- [Mainboard moulded marking](../photos/05-switch-mainboard-connector-marking.jpg)

All photos are from the hardware owner; third-party marketing imagery is excluded.
