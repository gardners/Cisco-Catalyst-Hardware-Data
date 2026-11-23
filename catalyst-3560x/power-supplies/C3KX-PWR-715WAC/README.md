# Cisco C3KX-PWR-715WAC factory power-supply module

## Inspected labels

- Cisco designation: `C3-KX-PWR-715WAC V01` (observed label), Cisco accessory family `C3KX-PWR-715WAC`.
- Lite-On OEM: **`PA-1711-1-LF REV:04`**.
- Delta OEM: **`EDPS-715AB`**.

## Published ratings, not verified electrical measurements

| Property | Cisco rating |
|---|---|
| Maximum power | 715 W |
| DC output | **−56 V / 12.8 A** |
| AC input | 100–240 V AC; 50/60 Hz |
| Enclosure dimensions (H×D×W) | ~35 × 260 × 83 mm |

Cisco publishes the voltage as **−56 V**, not +56 V. The blade assignments, return reference, chassis earth relationship, standby rails, enable conditions and hot-swap sequencing are unknown.

## Factory output connector

Observed interface: **two substantial DC blade contacts plus sixteen smaller control/signal contacts**. Guide feature centres were measured approximately 30 mm apart (~25.5 mm inside-edge gap). An Amphenol PwrBlade 1P+16S+1P part resembles this interface. This is a **candidate**, not a verified manufacturer identification or interchangeable part; see [connector investigation](connector.md).

The factory motherboard is ~2.4 mm thick at the interface. Its sockets appear flush with the PCB edge near holes H07/H08; see the **provisional and explicitly marked socket overlay** in [mainboard survey](../../mainboard/README.md).

The 16 small contact functions are **not known**. [Pin investigation worksheet](connector-pinout-worksheet.csv) remains open; no pin may safely be assumed power-good or PS-ON.

## Source documents

- [Cisco technical specifications](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3750x_3560x/hardware/installation/guide/3750x_3560x_HIG/HIGSPEC.html)
- [Cisco power module service guide](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3750x_3560x/hardware/install/notes/pwr_note.html)
- [Amphenol PwrBlade 51760-10101601AALF candidate](https://www.amphenol-cs.com/product/5176010101601aalf.html)

**Warning:** This AC module contains hazardous mains circuitry and stores energy. No verified independent enable or bench-power procedure is supplied here.
