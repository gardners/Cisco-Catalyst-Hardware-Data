# Factory fan cartridges — C3KX-FAN-23CFM

Cisco's Catalyst 3560-X / 3750-X generation chassis has **two replaceable fan cartridges**, each with two fans (four fans per chassis when both cartridges are populated). The fan modules and the **fans built into the power-supply modules** are different assemblies.

| Identification | Observed / documented detail | Confidence |
|---|---|---|
| Cisco cartridge | `C3KX-FAN-23CFM` | Cisco service documentation |
| Fan motor marking | **Delta `GFC0412DS-9G28R`** | owner's observed marking |
| Electrical label | **12 V, 1.20 A** | observed motor label; not independently measured |
| Cartridge connector pin count/pinout | **Unknown** | no verified wiring documentation |
| Fan speed control method | **Unknown on this cartridge** | do not assume a conventional PC 4-wire pinout |

The exact winding configuration, tach/PWM behaviour, minimum speed and power-on fail-safe have not been measured. The cartridge connector is considered a **proprietary/unidentified** interface until electrically traced. [Connector worksheet](fan-connector-worksheet.csv) and [bench observations to collect](bench-tests.md) are retained.

## Manufacturer documentation

- [Cisco removable fan modules](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3750x_3560x/hardware/installation/guide/3750x_3560x_HIG/HIGFRU.html)
- [Cisco fan module installation note](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3750x_3560x/hardware/install/notes/fan_note.html)
