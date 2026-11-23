# Original motherboard survey: method and provenance

## Hole fitting

A set of **53 independent/partly redundant** maximum-separation caliper readings between mounting holes H01–H19 were collected on the removed motherboard. Three cross-checks against a ruler suggested the particular jaw-in-hole technique gave a **3.5 mm systematic extra spread**, which was subtracted to estimate centre distances. A nonlinear least-squares fit placed the 19 centres relative to a fixed H01–H04 ruler baseline (103, 185, 267 mm from H01); the observed underside photograph selected the mirror orientation.

Numerical fit RMS residual: **0.159 mm** across the 53 comparisons; largest absolute residual **0.500 mm**. This measures consistency with a model and assumptions, not calibrated hole coordinate accuracy. Independent visually observed near-collinearity relationships were deliberately **not** added as constraints. This export reproduces the final fitted hole coordinates, but **does not claim to include a separately retrievable full 53-line raw reading sheet**.

## PCB rim-to-edge conversion

The investigator reported distances from each hole's *nearest rim* to nearby local board edges. Subtract/add an assumed 1.875 mm hole radius (provisional Ø3.75 mm) to convert to centre-relative edge-plane positions. Repeated observations support several parallel edge planes (see CSV), while corners and step transitions are less secure. H11 lower shoulder near Y=148.96 mm, H14 local laminate edge around Y=248–249 mm and H18 rear Y≈338.02 mm were subsequently supplied and used where relevant.

## PSU connectors

A separate two-photograph investigation of the original motherboard solder-tail positions compared them against an **Amphenol PwrBlade 51760** family mechanical drawing. The two small board-lock joints, not the larger chassis supports H07/H08, were used for alignment. The candidate drawing predicts board-lock pitch 31.75 mm and local board-edge setback 6.35 mm. Horizontal offsets ~11 and ~102 mm from the local left side were photographic estimates, not verified caliper measurements. Converting to the H01-relative frame assumes this 'local left side' is the upper-left fitted X plane (−13.13 mm), and that the mating edge corresponds to the H07/H08 Y=87.60 shoulder. Both registration assumptions may require correction.

This is **only a mechanical hypothesis overlay**: no drill footprints or contact land patterns were generated. Please measure an original socket, confirm original header/receptacle gender and mechanically fit a sample before using the part in hardware.

## Orientation and project-independent scope

The original coordinate convention (underside X right, Y rearward) has been preserved for traceability and mirrored to KiCad's top view. This archive only records **original Cisco hardware**, including tentative identifications, and contains no new appliance circuitry.
