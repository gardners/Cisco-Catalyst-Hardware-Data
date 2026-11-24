# C3KX-NM-10G — Cisco IOS PHY observability opportunities

Date: 2026-11-25. Status: `VENDOR` command documentation, **NOT** verified on the owner's switch/module.

## Available test hardware / future exploration

Owner confirmed 2026-11-25: a working 24-port Catalyst 3750 with a C3KX-NM-10G installed is available. Exact switch PID and IOS version remain to be recorded. This pathway is deferred until bench access is convenient; no test results yet. Prioritize non-invasive IOS diagnostics, then passive MDIO capture if the CLI does not reveal numeric transactions.

## Why investigate IOS before invasive reverse engineering?

Cisco's Catalyst 3750-X/3560-X command reference documents privileged EXEC `show controllers ethernet-controller ... phy [detail]`, and `debug platform phy` categories including `init-seq`, `read`, `write`, `sfp`, `link-status`. These may reveal module-specific PHY initialization/management events or register transactions. Whether C3KX-NM-10G-specific Clause 45 BCM8727 accesses are actually passed through the generic debug hooks is **unknown**. A publicly posted C3KX-NM-10G `show controllers ... phy` capture primarily reports SFP+ serial EEPROM, not a full PHY register dump. Do not claim the diagnostic commands themselves disclose BCM8727 register addresses until tested.

## Confirmed command syntax (Cisco 3560-X / 3750-X documentation)

```
show controllers ethernet-controller tengigabitethernet1/1/1 phy
show controllers ethernet-controller tengigabitethernet1/1/1 phy detail
debug platform phy init-seq
debug platform phy read
debug platform phy write
debug platform phy link-status
debug platform phy sfp
```

Use the actual installed interface identifiers (`show interfaces status`, `show interfaces description`, or `show ip interface brief`), not the example numbers blindly. Per-interface `show controllers ... phy` syntax may be accepted while `debug platform phy` is **global**, not per-port.

## Low-risk bench sequence

1. With module installed in an otherwise isolated donor switch, note `show version`, `show inventory`, `show interfaces status`, and `show logging`. Record exact IOS release, module PCB revision if known, interface names and transceiver types. Mask device serials before publishing.
2. Capture ordinary `show controllers ethernet-controller ... phy` / `phy detail` for both a Gx 1G interface and a 10G-capable interface, if available. Record precise CLI errors, if unsupported.
3. Only on a bench switch, enable one debugging category at a time and capture the command's output. `debug platform phy init-seq`, `read` and `write` can create voluminous logs or performance impact. Prefer local console logging, rather than risking a flooded remote session. Confirm buffer settings and the ability to stop debugging first.
4. A port `shutdown`/`no shutdown`, SFP insertion, or media change might cause link events, but it is **not proven** to re-run external PHY power-on or SPI ROM boot. Avoid using a disruptive module reinsert or switch reboot until necessary and only on isolated hardware.
5. Disable the category after each short capture: `no debug platform phy read`, etc. `undebug all` is appropriate only if you own the entire bench switch's debug state; on shared switches it would cancel other people's debugging.
6. Compare log content in four conditions: no SFP; 1G SFP in G1/G3; 1G SFP in G2/G4; 10G SFP+ in G2/G4. Note that Cisco's pairing restrictions make some simultaneous combinations invalid.

## If MDIO register access appears in logs

Log fields: timestamp, IOS version, module type, logical port, PHY address, MDIO devad, register, read/write, written value/read value, preceding trigger, confidence. Do not call a port identifier an MDIO address without evidence. Map recovered numeric register addresses against `components/BCM8727/BCM8727_register_map.csv`, using `S` for released driver comparison and a **separate** notation for Cisco-measured debug output.

Useful known candidates from Linux BCM8727/BCM8722 support (not proof Cisco uses same setup): devad 1 (`PMA/PMD`), `0xC800` (PHY identifier / control register, **not** IEEE standard PHY ID), `0xCA10` (general control), `0xCA85` (misc control 1), `0xCA19` (firmware ROM version 1). See associated BCM8727 note.

## Public references

- Cisco, *Catalyst 3750-X and 3560-X Switch Command Reference*, `show controllers ethernet-controller`: https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3750x_3560x/software/release/15-0_2_ez/command/reference/3750xcr/cli2.html
- Cisco, *Catalyst 3750-X and 3560-X Switch Debug Commands*, `debug platform phy`: https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3750x_3560x/software/release/15-0_2_se/command/reference/3750xcr/debug.html
- Example C3KX-NM-10G `show controllers ... phy` output (community, not independent verification of chip register access): https://community.cisco.com/t5/switching/10gb-link-between-2-3750x-switches-with-c3kx-nm-10g-modules/m-p/4485016/highlight/true

## Evidence limitations

No live IOS capture was obtained by this document's author. This is a prioritized data-acquisition plan, **not** a recovered Cisco initialization sequence. No claims about actual module connector pin assignments.
