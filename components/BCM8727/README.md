# Broadcom BCM8727 — open-source technical datasheet

Independent, **incomplete** technical reference built from Broadcom's public product brief, Terasic's real-world reference design, Intel's interoperability reference and upstream Linux PHY drivers. It is not an official Broadcom datasheet, nor is the package pin mapping complete.

- [Latest compiled datasheet (PDF)](BCM8727_Open_Source_Datasheet.pdf)
- [LaTeX source](BCM8727_Open_Source_Datasheet.tex)
- [324-position BGA signal register](BCM8727_BGA_324_ball_register.csv)

This repository is the **canonical location for the latest version**. Source contains evidence classes P (Broadcom), R (reference design), S (driver), I (inference) and U (unavailable). 110 balls are mapped to public reference-design signals; 214 ball locations remain unknown, **not NC**. The complete power/ground map is not public; do not use this document as an unverified production fabrication specification.

Build with `make`, requiring `pdflatex` and TeX packages including `sourcesanspro`.

The installed Cisco C3KX-NM-10G sled is documented separately at [the network-module section](../../catalyst-3560x/network-modules/C3KX-NM-10G/README.md). The chip datasheet intentionally does **not** contain Cisco-specific pin mappings or connector wiring.
