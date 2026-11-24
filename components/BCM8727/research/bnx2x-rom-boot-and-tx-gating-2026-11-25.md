# BCM8727 — external serial-ROM boot and dual TX-enable controls

Date: 2026-11-25. Status: `S` released Linux driver evidence; `VENDOR` Broadcom-authored 2012 patch; applicability to **Cisco's** C3KX-NM-10G not established.

These details complement, rather than replace, the repository's revision 0.3 independent datasheet/register CSV.

## 1. SPI serial-ROM firmware loading is supported in BCM8727 designs

Linux `bnx2x_link.c` has `bnx2x_8073_8727_external_rom_boot()`, called by `bnx2x_8727_common_init_phy()` in applicable Broadcom network-card designs. The routine:

- On Clause 45 MMD 1 (PMA/PMD), writes `GEN_CTRL` (`0xCA10`) values `0x0001`, `0x008C`.
- Writes `MISC_CTRL1` (`0xCA85`) value `0x0001` to set serial boot control.
- Writes `GEN_CTRL` (`0xCA10`) values `0x018A` (ROM micro reset) then `0x0188` (release internal microprocessor reset).
- Delays ~100 ms; polls `ROM_VER1` (`0xCA19`) and `M8051_MSGOUT_REG` (`0xCA13`). A version of `0` or `0x4321` continues polling; the extra low-byte message check (`0x03`) applies to BCM8073 in this shared routine.
- Writes `MISC_CTRL1` (`0xCA85`) value `0x0000` to clear serial boot control.

This implies an external SPI-ROM image can be important to PHY function on such hardware. The Broadcom product brief likewise documents an embedded controller and external SPI interface. **It does not establish whether Cisco populates an external ROM** on the C3KX-NM-10G; a board-specific photograph/continuity check is required. It also does not license copying the register-write sequence blindly into our hardware; reset timing, supplies and clock must be established first.

### Bench priority

Identify all 8-pin serial flash/EEPROM candidates near the BCM8727; record the exact part numbers and trace `/CS`, `SCK`, `MOSI`, `MISO` to known BCM8727 SPI pins or intermediate components. If a genuine serial firmware flash exists, consider a **read-only, in-circuit-safe** dump with power removed; do not apply independent 3.3 V or drive signals into a powered/unpowered board without establishing supply domain and contention first. Preserve the original bytes and hashes.

## 2. Optical TX enable can be gated in two places

Broadcom's 4 April 2012 Linux netdev patch describes BCM57712 + BCM8727 designs where a GPIO and a separate MDIO-controlled PHY control are logically ANDed before the laser transmits. After older software disabled the MDIO control, changing the GPIO alone did nothing.

`MDIO_PMA_REG_PHY_IDENTIFIER` is **vendor register MMD1:0xC800**, not IEEE-defined PMA PHY-ID register `MMD1:0x0002/0x0003`. In the released `bnx2x_link.c` `bnx2x_sfp_set_transmitter()` path, `0xC800` bit 15 is cleared to permit transmission and set to inhibit it (when `PORT_HW_CFG_TX_LASER_MDIO` selects the MDIO control). The 2012 patch explicitly clears bit 15 in its initialization path to avoid a TX-disable latch left by old software. Do not use this as proof of exact Cisco wiring.

### Bench priority

Trace SFP+ cage `TX_DISABLE` towards GPIO buffers/supervisor logic and BCM8727 control; identify whether the control is directly attached to FPGA/switch-host module contacts or is processed locally. Check for both PHY and cage enable conditions before concluding a nontransmitting port means a bad XAUI/SerDes link. Do not enable a laser outside a safe, terminated optical setup.

## 3. Additional BCM8727 speed-selection evidence

The released `bnx2x_8727_config_speed()` path deliberately handles 1G SFP fibre: when speed is forced to 1000 Mb/s or `media_type == ETH_PHY_SFP_1G_FIBER`, it writes PMA/PMD control `MMD1:0x0000 = 0x0040` and 10G control 2 `MMD1:0x0007 = 0x000D`, then reads `MMD1:0x0007` back. For dual-media designs, it can set bits `[11:10]` of `MMD1:0xC842` (`8727_PCS_GP`) to power down XAUI pending link.

Interpretation: released code provides a concrete **1G-through-BCM8727** mode on supported Broadcom designs. This strengthens the hypothesis that Cisco's two dual-rate G2/G4 cages *could* traverse BCM8727 in both speeds. It says **nothing** about the two additional G1/G3 1G-only cages, their host routing, or Cisco's exact mode switching.

## 4. References

- Linux `bnx2x_link.c`, functions `bnx2x_8073_8727_external_rom_boot`, `bnx2x_8727_config_speed`, `bnx2x_sfp_set_transmitter`: https://codebrowser.dev/linux/linux/drivers/net/ethernet/broadcom/bnx2x/bnx2x_link.c.html
- Linux `bnx2x_reg.h`, vendor register definitions (0xC800, 0xCA10, 0xCA13, 0xCA19, 0xCA85, 0xC842): https://codebrowser.dev/linux/linux/drivers/net/ethernet/broadcom/bnx2x/bnx2x_reg.h.html
- Yaniv Rosner (Broadcom), 4 Apr 2012, `[net 06/10] bnx2x: Fix link issue for BCM8727 boards`: https://lists.openwall.net/netdev/2012/04/04/109
- Broadcom BCM8727 product brief: https://docs.broadcom.com/doc/12358272

## Evidence limitations

The `bnx2x` routines configure the BCM8727 in Broadcom/QLogic NIC reference designs and are not a complete or verified initialization sequence for the Cisco module. MDIO/firmware/laser control assignments should retain their source and confidence labels in any integrated datasheet; avoid merging inferred Cisco board routing into confirmed silicon properties.
