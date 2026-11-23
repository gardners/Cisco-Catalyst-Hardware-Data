# C3KX-NM-10G host connector: component identification and sourcing

**Status checked: 24 November 2026.** Inventory and prices may change. This page is about the **Cisco switch motherboard-side host connector**, whose central 192-contact signal insert and outer eight-power-contact overlay are **separate pieces**. The two observed assembly markings must not be conflated with the signal insert's orderable part number.

## Confidence labels

- **TE verified** — manufacturer identifies the component or explicitly lists the mate in its catalogue/drawings.
- **Observed** — printed/moulded identification and mechanical structure present in owner-supplied photographs; may be a moulding number rather than a separately orderable assembled SKU.
- **Distributor offer** — supplier lists the stated part; stock, minimum order quantity and prices must be checked at order time.
- **Broker lead** — inventory directory or RFQ advertisement, not independently verified as on-hand stock or an authorised channel.
- **Unconfirmed** — no manufacturer drawing, verified part record or interchangeability established.

## Connector components

| Physical item | ID / TE part number | Status | Notes |
|---|---|---|---|
| Motherboard **signal header**, 192 contacts | **1934318-1** | **TE verified / distributor offers** | 12 × 16 positions, vertical, through-hole press-fit TinMan header. TE's mating table lists it as a mate to 1934225-1. Not yet conclusively established as the SKU actually mounted on the Cisco motherboard. |
| Motherboard **power guide/overlay** with eight larger contacts | **1926945-1** (moulded marking) | **Observed; sourcing unknown** | Owner's macro photo shows `1926945-1` and `1126 STD`. Likely a Cisco-specific combined housing/contact subassembly; do not assume moulding number is standalone orderable SKU. |
| Power header **possible suffix variant** | **1926945-2** | **Broker lead; unconfirmed substitute** | AAA Connectors lists `TE Conn Backplane HDR 8Power`. No TE drawing found to establish differences vs. `-1`. Request photos and drawing before ordering. |
| Sled **signal receptacle**, 192 contacts | **1934225-1** | **TE verified** | Signal mating half; 12 × 16 positions, right-angle TinMan receptacle. |
| Sled **power guide/overlay** | **1926944-1** (moulded marking) | **Observed; sourcing unknown** | Owner observed Tyco Electronics mark on the power/blade shroud. Distinct from 1934225-1. |

### Published intermate confirmation

TE's Z-PACK TinMan catalogue (5-1773447-9, 2007) explicitly lists vertical header **1934318-1** as mating with right-angle receptacle **1934225-1**. This proves compatibility **for the 192-position signal section only**. It does **not** establish the match, pinout, voltage rating or contact sequence of the eight power contacts, nor does it prove the exact Cisco motherboard signal-core SKU.

Manufacturer data: [TE signal header](https://www.te.com/en/product-1934318-1.html), [TE signal receptacle](https://www.te.com/en/product-1934225-1.html), [TinMan catalogue, mating table](https://datasheet.octopart.com/1934222-1-TE-Connectivity-datasheet-5316232.pdf).

## Supplier leads

| Item | Supplier / search | What could be verified | Caveat |
|---|---|---|---|
| 1934318-1 | [DigiKey Australia](https://www.digikey.com.au/en/products/detail/te-connectivity-amp-connectors/1934318-1/4021741) | Catalogue item `A107860-ND`, small-quantity listing and marketplace seller offers | Verify seller, origin, quantity and delivery. Manufacturer-stock listing has at times shown just one unit. |
| 1934318-1 | [Win Source](https://win-source.net/category/memory-cards-modules/specialized/6) | Distributor inventory listed 105 pieces in search results | Broker stock must be confirmed. |
| 1934318-1 | [Mouser](https://www.mouser.com/ProductDetail/TE-Connectivity/1934318-1) | Orderable catalogue page and factory-lead-time information | Page showed **non-stocked**, MOQ **540**; inconvenient for prototypes. A distributor short description differed from TE's own part description: use the manufacturer drawing. |
| 1934318-1 | [RS Americas](https://us.rs-online.com/product/te-connectivity/1934318-1/72136017/) | Catalogue/quote listing | Backorder and large MOQ (180) on checked listing. |
| 1934318-1 | [OEMsTrade results](https://www.oemstrade.com/search/43181) | Aggregated distributor offers | Search results may contain non-exact matches; validate manufacturer number. |
| **1926945-1** | [Octopart exact-part search](https://octopart.com/search?q=1926945-1) | Search-only route | **No verified seller or manufacturer page found** for exact `-1`. Not evidence of stock. |
| **1926945-2** | [AAA Connectors inventory](https://www.aaaconnectors.com/en/products/inventory-1.html) | Lists `1926945-2 TE Conn Backplane HDR 8Power` | Broker **lead**, not verified stock or compatible alternative to `-1`. |
| 1926945-2 | [Octopart search](https://octopart.com/search?q=1926945-2) | Search-only route | No verified Octopart product listing established. |
| 1934225-1 | [TE product listing](https://www.te.com/en/product-1934225-1.html) | Manufacturer status and drawings | This is the **sled** signal half; not the requested motherboard part. |

**No current complete-motherboard-connector procurement source has been confirmed.** An individually obtainable 1934318-1 does not solve the eight-contact power section.

## Identification / purchase checks before paying for an overlay

1. Obtain TE's original customer drawing for **1926945-1** and **1926945-2**, or obtain TE engineering confirmation that the moulded `-1` marking is an orderable finished assembly number and whether `-2` is an approved substitute.
2. Confirm power-pin positions, male/female orientation, guide/keying, contact sequencing and the contact-to-PCB footprint. The original Cisco board appears to have an array of power contact plated-through holes flanking the signal area; the overlay's attachment method is **not** yet established.
3. Confirm which parts are included: plastic body, power blades, any grounding contacts, and mounting/press-fit retention features. A loose shell without contacts is insufficient.
4. Compare official customer drawings against the 24-Nov-2026 owner photos. Request seller photos of **the actual stock and its part markings**, not a catalogue thumbnail.
5. Do not assume the moulding part number identifies the complete factory-assembled TE SKU. TE may need to search internal drawings or the original Cisco BOM to identify it.

## Possible practical alternatives

- **Salvage the complete motherboard overlay** if commercially unavailable. Mechanical extraction may be possible, but mixed connector sections may have different press-fit/solder attachment mechanisms and recovered contacts are not automatically qualified for reuse.
- **Mate the 192 signal pins with a new 1934318-1**, and supply the sled power contacts through a separately engineered, mechanically verified solution. This is *not* a drop-in replacement for the original Cisco receptacle assembly; respect hot-plug sequencing and mechanical alignment.
- Ask TE support to identify any **replacement overlay or complete connector assembly** using both observed markings `1926944-1` and `1926945-1` and a photograph of each part.

## Photographs, in this repository

- [Mainboard component-side moulded marking](../photos/05-switch-mainboard-connector-marking.jpg)
- [Mainboard signal contact footprint](../photos/06-mainboard-header-pressfit-footprint-closeup.jpg)
- [Mainboard routing and component fan-out](../photos/07-mainboard-header-trace-fanout.jpg)
- [Sled connector face](../photos/03-module-connector-mating-face.jpg)

All photos referenced here were supplied by the hardware owner, not copied from an unrelated third-party listing.
