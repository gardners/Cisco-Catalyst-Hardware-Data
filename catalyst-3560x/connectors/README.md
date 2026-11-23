# Connector and unusual interface index

This is an **identification register** for the original Cisco assemblies. A part listed as CANDIDATE is not a recommendation to fit that part. There are no verified supplier footprints for the proprietary assemblies yet.

| Original assembly / interface | Observed form | Identified part or investigation lead | Status |
|---|---|---|---|
| C3KX-PWR-715WAC DC motherboard interface (×2) | 2 wide blades + 16 signal contacts; board-edge right angle; two guides ~30 mm apart | Amphenol PwrBlade `51760-10101601AALF` receptacle; advertised mate `51720-10101601AALF` | **CANDIDATE** (not matched by sample) |
| Two PSU socket board-locks | ~31.75 mm candidate pitch; ~6.35 mm edge setback | Derived from candidate manufacturer's mechanical drawing registered against two photos | **HYPOTHESIS** |
| Factory front-panel J2 | Narrow 20-contact surface-mount board-to-board/cable connector, photo available | Manufacturer, pitch and exact mate unknown | **UNIDENTIFIED** |
| Factory front-panel J1 | USB Mini-B female panel socket | USB Mini-B connector type known; OEM SKU unknown | **TYPE KNOWN / PART UNKNOWN** |
| Front-panel SW1 | Four-land momentary switch footprint (unpopulated on specimen) | Mechanical series/actuator profile unknown | **UNIDENTIFIED** |
| `C3KX-FAN-23CFM` cartridge | Proprietary replaceable fan-cartridge edge/header connection | Manufacturer, pinout and mate unknown | **UNIDENTIFIED** |
| Network module (`C3KX-NM-10G`) | Removable module connector to switch mainboard | Cisco module SKU known; internal connector manufacturer/footprint unknown | **UNIDENTIFIED** |
| XPS 2200 rear power connection | Cisco external power system interface | Cisco XPS-2200 system identified; internal individual connector not surveyed | **UNSURVEYED** |
| StackWise/StackPower on 3750-X | Rear stack cable interfaces; not universal to 3560-X | Cisco family-specific external interfaces | **UNSURVEYED** |

## Vendor references

- [Amphenol 51760-10101601AALF specification](https://www.amphenol-cs.com/product/5176010101601aalf.html) — shows 2 power and 16 signal contacts and names its mate.
- [Cisco 3560-X / 3750-X ports and cabling](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3750x_3560x/hardware/installation/guide/3750x_3560x_HIG/HIGCABLE.html) — standard external USB/RJ45/module interfaces.
- [Cisco original module family](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3750x_3560x/hardware/installation/guide/3750x_3560x_HIG/HIGOVERV.html).

The PSU connector candidate is documented further at [C3KX-PWR-715WAC/connector.md](../power-supplies/C3KX-PWR-715WAC/connector.md), including size and mechanical alignment hypotheses.
