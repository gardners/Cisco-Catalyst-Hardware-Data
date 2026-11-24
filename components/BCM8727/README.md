# BCM8727 — independent open-source technical datasheet

**Revision 0.3 (25 November 2026)** — register-map expansion.

Canonical latest version: https://github.com/gardners/Cisco-Catalyst-Hardware-Data/tree/main/components/BCM8727

- [PDF](BCM8727_Open_Source_Datasheet.pdf) — datasheet (sans serif), engineering confidence markings, full 324-position BGA matrix and partial register tables.
- [LaTeX source](BCM8727_Open_Source_Datasheet.tex) — build with `make` or `pdflatex`.
- [BCM8727 partial register map (CSV)](BCM8727_register_map.csv) — 21 observations / registers; repeated entries may capture both baseline and experimental evidence.
- [Comparative PHY registers (CSV)](COMPARATIVE_PHY_register_candidates.csv) — **NOT BCM8727 assignments**; register candidates from related copper PHYs.
- [324-ball position inventory](BCM8727_BGA_324_ball_register.csv) — 110 named from Terasic, 214 unknown; unknown does NOT mean NC.

## Evidence limits

`P`: published Broadcom brief. `R`: Terasic reference design. `S`: released driver. `X`: experimental patch. `C`: a different PHY used only as a comparator. `I`: inference. `U`: unknown.

2.5G claims rely on proposed Linux/FreeBSD patches plus host Warpcore settings; manufacturer support and other hosts/suffixes are **unconfirmed**. The register tables are incomplete (bit definitions and defaults often unknown). The copper PHY registers must not be written to the BCM8727 on the strength of this comparison.

## Repository integration

This directory contains only generic BCM8727 data, not Cisco-specific module connector pins. The Cisco network-module board is covered separately in `catalyst-3560x/network-modules/C3KX-NM-10G/`.

**Incremental archive:** package is intentionally scoped to `components/BCM8727/` so it does not replace unrelated PSU/chassis work. Review conflicts if other authors touched these same chip datasheet files.

## Build

```sh
make
```

TeX prerequisites: `pdflatex`, Source Sans Pro TeX support, and usual `booktabs`, `longtable`, `hyperref`, `fancyhdr` packages. The PDF is generated from the TeX source; original vendor PDFs and GPL driver code are not embedded.
