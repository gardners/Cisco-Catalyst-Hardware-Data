# Primary references and software

| Source | Content |
|---|---|
| [Cisco network-module installation notes](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3750x_3560x/hardware/install/notes/net_mod_note.html) | Port pair constraints; module and host support |
| [Cisco Catalyst 3750-X/3560-X data sheet](https://www.cisco.com/c/en/us/products/collateral/switches/catalyst-3560-x-series-switches/data_sheet_c78-584733.html) | Module family and SKUs |
| [Broadcom BCM8727 product brief](https://docs.broadcom.com/doc/12358272) | Chip architecture, interface rates and power |
| [Terasic Dual XAUI to SFP+ HSMC manual](https://datasheet.ersaelectronics.com/static/datasheets/terasic/terasic-p0092.pdf) | Public BCM8727 ball assignments, oscillator/board reference |
| [Intel AN638](https://cdrdv2-public.intel.com/655128/an638.pdf) | FPGA and BCM8727 interoperability test |
| [Linux bcm87xx.c](https://codebrowser.dev/linux/linux/drivers/net/phy/bcm87xx.c.html) | MDIO identification, status, alarms |
| [Linux bnx2x_link.c](https://codebrowser.dev/linux/linux/drivers/net/ethernet/broadcom/bnx2x/bnx2x_link.c.html) | BCM8727-specific register sequences and 1G/SFP controls |
| [Linux BCM87xx device tree binding](https://github.com/torvalds/linux/blob/master/Documentation/devicetree/bindings/net/broadcom-bcm87xx.txt) | Optional Clause45 register init tuples |
| [TE 1934225-1 product page](https://www.te.com/en/product-1934225-1.html) | Confirms 192-position Z-PACK TinMan right-angle signal receptacle and press-fit termination |
| [TE 1934318-1 product page](https://www.te.com/en/product-1934318-1.html) | Compatible 192-position signal header candidate; exact Cisco-mounted part remains unverified |
| [TE TinMan application specification 114-13202](https://www.farnell.com/datasheets/1922330.pdf) | Contact insertion, tooling, PCB support and repair/replace constraints |
| [Surplus part inventory mentioning 1926945-2](https://www.aaaconnectors.com/en/products/inventory-1.html) | TE header 8Power reference; **not proof of -1 pinout or stock** |

**Note:** Datasheets and third-party photos are linked, not mirrored here. The repository is limited to hardware measurement data, owner photos, and independent written observations.
