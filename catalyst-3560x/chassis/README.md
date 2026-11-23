# Factory chassis — 3560-X / 3750-X generation

The specimen is a 1RU 24-port PoE+ Catalyst chassis. Its exact model and manufacturing revision are to be confirmed from its serial label. Vendor-published specifications vary with port count and PoE configuration.

| Property | Recorded figure | Source / limitation |
|---|---:|---|
| Nominal enclosure height | 44.5 mm | Cisco technical specifications |
| Nominal body width | 445 mm | Cisco, excluding rack ears |
| Nominal depth, typical 24-port model | 460 mm | Cisco; other variants can be 495 mm |
| Estimated usable interior vertical clearance | ~40 mm | Owner observation; check near lid/pressed metal |
| Approximate front-to-rear interior region | ~400 mm | Owner estimate, not a cavity CAD |
| Clear electronics-side region | ~250 mm wide × ~300 mm deep | Owner estimate; local to region |
| Front-to-PSU intrusion distance | ~140 mm | Owner estimate **on PSU side only** |
| Original mainboard mounting bosses | ~6 mm tall | Owner estimate; each boss needs confirmation |
| Original board nominal thickness | ~2.4 mm | Owner measurement |

The factory front fascia was observed to have five structural areas, approximately **80 + 90 + 90 + 90 + 90 mm** across. The four ~90 mm areas have an upper ventilation region approximately 8 mm tall and a lower ~5 mm light-pipe region; the ~80 mm area has six upper light pipes. **24 lower light pipes** were observed in four groups of six. Pipe centre-to-centre positions, lower-PCB LED coordinates and board-side offsets remain to be measured. These are observations of the Cisco original; no replacement front-panel proposal is part of this repository.

The chassis retains two rear PSU bays and two fan cartridge positions. Cisco documents the appropriate power-supply blank covers and airflow practices.

The original motherboard's H01–H19 coordinates and non-rectangular perimeter are recorded **separately** in [the mainboard mechanical survey](../mainboard/README.md). Chassis-wall registration and which through-holes correspond to usable bosses have not been completely confirmed.

## References

- [Cisco hardware specifications](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3750x_3560x/hardware/installation/guide/3750x_3560x_HIG/HIGSPEC.html)
- [Cisco PSU/fan service arrangements](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3750x_3560x/hardware/installation/guide/3750x_3560x_HIG/HIGFRU.html)
