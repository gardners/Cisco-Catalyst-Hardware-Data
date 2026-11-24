# BCM8727 open-source technical datasheet — change history

## Revision 0.3 — 25 November 2026

- Added Clause 45 register address inventory recovered from Linux `bnx2x` and `bcm87xx` (21 source-labelled rows, including experimental aliases). The map intentionally leaves undocumented bitfields and reset defaults unspecified.
- Recorded baseline 1G and 10G register writes and explicit 2.5G experimental settings for MMD 7 offsets `0x8308`, `0x8309`. The experimental implementation also reconfigures **host Warpcore SerDes**, not only the BCM8727.
- Added SFP EEPROM bridge/control register addresses, vendor optics controls, PCS/XGXS/LASI status, and source-level evidence for reset/mode control.
- Added 9 separate register comparisons from **different** Broadcom copper PHYs. These are not BCM8727 assignments and must not be used as if they were.
- Added FreeBSD `bxe` review references (D40358 host and D40359 PHY), DPDK lineage, and OpenBSD/NetBSD/ReactOS driver coverage limitations.
- Kept complete 324-BGA-position class map: 110 Terasic-named, 214 explicitly unknown. Reworked landscape page to keep matrix with its heading.
- Updated source references, revision metadata and the pointer to the canonical GitHub repository.

**Evidence caveat:** Driver-source register writes establish that code targets an address; they do not constitute manufacturer electrical specifications or proof of operation on every suffix/firmware build. An unmerged patch can contain genuine engineering insight without having been qualified upstream.

## Revision 0.2 — 24 November 2026

Original independent reference with published PHY characteristics, Terasic BGA signal inventory, reference designs and upstream Linux link-status source references.
