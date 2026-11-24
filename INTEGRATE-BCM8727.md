# BCM8727 datasheet integration candidate (2026-11-25)

The accompanying research note is intended as normative content for the independent datasheet, subject to its evidence labels, rather than merely a future experiment. The current LaTeX source and register CSV could not be fetched in this session. No existing files are replaced and no revision number is asserted.

Suggested placement: firmware/initialization, transmitter control, speed selection, and register descriptions. Compare against existing rows before merging; these observations are not necessarily all new addresses. Do not infer individual bitfields from whole-register write constants.

| MMD | Register | Observed operation | Evidence / qualification |
|---|---|---|---|
| 1 | 0xCA10 | Write 0x0001, 0x008C; after serial boot enable write 0x018A, 0x0188 | Released bnx2x shared 8073/8727 external ROM boot routine; last pair resets/releases microcontroller. |
| 1 | 0xCA85 | Write 0x0001 before microcontroller reset, 0x0000 after polling | Serial boot control; other bits unknown. |
| 1 | 0xCA19 | Read; 0 and 0x4321 treated as not ready | ROM version 1, driver readiness heuristic. |
| 1 | 0xCA13 | Read during shared boot polling | M8051 message out; low-byte 0x03 completion check is 8073-specific in this routine. |
| 1 | 0xC800 | Bit 15 set inhibits TX, clear permits TX | Vendor PHY identifier/control, not standard ID; conditional MDIO laser-control path. |
| 1 | 0x0000 | Write 0x0040 | Forced 1G fibre configuration. |
| 1 | 0x0007 | Write 0x000D, read back | Forced 1G fibre configuration. |
| 1 | 0xC842 | Set bits 11:10 conditionally | XAUI power control in dual-media designs; not proof of Cisco routing. |

Full sequence, source references and limitations: `components/BCM8727/research/bnx2x-rom-boot-and-tx-gating-2026-11-25.md`.

Module-specific deferred test pathway: `catalyst-3560x/network-modules/C3KX-NM-10G/research/ios-phy-observability-2026-11-25.md`.
