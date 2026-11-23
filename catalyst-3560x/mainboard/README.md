# Original Cisco mainboard mechanical survey

A coordinate-registered, editable **historical original-board** mechanical survey: 19 mounting-hole centres from a 53-distance fit, local measured PCB-edge planes, and two PSU connector **candidate** locations from a separately photo-registered Amphenol footprint investigation. This is not a new PCB design or an assertion that all Catalyst 3560-X and 3750-X motherboards are interchangeable.

## Files

- [`kicad/cisco-mainboard-mechanical-survey.kicad_pcb`](kicad/cisco-mainboard-mechanical-survey.kicad_pcb): top-view KiCad mechanical board **template**, with provisional closed `Edge.Cuts` outline and non-drilling reference circles for H01–H19, PSU socket **hypothesis** alignment marks on `Dwgs.User`.
- [`figures/mainboard-underside-survey.svg`](figures/mainboard-underside-survey.svg): **original underside orientation** with identified H-series centres and overlay connector board-lock locations.
- [`figures/mainboard-top-view-survey.svg`](figures/mainboard-top-view-survey.svg): **mirror image of original underside** for KiCad editing (also available [PNG](figures/mainboard-top-view-survey.png)).
- [`mounting-hole-centres-underside.csv`](mounting-hole-centres-underside.csv): original relative survey values to 0.001 mm computational precision, not physical accuracy.
- [`mounting-hole-centres-kicad-top-view.csv`](mounting-hole-centres-kicad-top-view.csv): mapped KiCad coordinates with explicit transform.
- [`edge-plane-register.csv`](edge-plane-register.csv): measured rim-derived edge planes and later added edge measurements, with source confidence.
- [`psu-socket-hypotheses.csv`](psu-socket-hypotheses.csv): **unverified** connector geometry registered to a possible local edge.
- [`measurement-method.md`](measurement-method.md): raw procedure, assumptions and meaning of errors.
- [`light-pipe-led-positions-WORKSHEET.csv`](light-pipe-led-positions-WORKSHEET.csv): empty worksheet for the original 24 lower and six upper light-pipe positions; no coordinates invented.

## Reference system

User measurement view: **looking at the board from its underside**, front edge towards the viewer/top of diagram, X increasing rightward, Y increasing rearward. H01 = (0,0); H02=(103,0), H03=(185,0), H04=(267,0) mm are the ruler-fixed baseline.

KiCad is presented as a **top-side view**: `Xpcb=450−Xunder`, `Ypcb=100+Yunder` mm. This is a left/right mirror about the X datum; the 100 and 450 offsets simply keep the drawing in positive KiCad coordinates. All surveyed holes keep their H-series identifiers.

## Accuracy and release status

- 19 hole centres fitted to **53 original hole-to-hole maximum-spread caliper readings**, adjusted by an empirical **3.5 mm** method offset. RMS residual was **0.159 mm**, max 0.500 mm; neither number is guaranteed positional accuracy.
- Actual holes roughly **4 mm** across; the edge reconstruction used a provisional **3.75 mm** diameter for radius compensation, not a measured drill diameter. In KiCad these are **circles on `Dwgs.User`, not NPTH drills**.
- Original board outline is **stepped/hooked**, not rectangular. The front and local side/shoulder planes are backed by rim-to-edge data, but some bends are visually interpolated, including the front-right step's Y location. The rear edge near 338.02 mm was subsequently reported; rear/side transitions still need confirmation. The closed `Edge.Cuts` polygon is for **CAD viewing only**.
- The motherboard's ~2.4 mm thickness and ~6 mm original steel bosses were owner-observed, not supplier PCB stack specifications.
- `PSU-A` and `PSU-B` markers are **not verified positions**. The derived board-lock pattern is based on candidate connector drawing overlays: estimated feature X offsets 11/102 mm relative to the local left plane, 31.75 mm feature pitch, 6.35 mm edge setback, approx 91 mm socket-to-socket pitch. Neither socket tail drills nor copper patterns have been placed.
- PCB relative coordinates are not yet fully **registered to chassis sheet-metal walls**. Verify model, front/side offsets and the bosses before using a board as a cutting/drilling template.

## Later addition: original underside front light-pipe LED positions

The front chassis has **24 lower light pipes (four groups of six)** and six upper pipes near the console board. Their actual emitting LED footprints **on the underside of the original Cisco mainboard** have not been surveyed. The KiCad template deliberately leaves them absent. Once the light-pipe positions and board-side orientation are measured, add their coordinates to a separate documented layer and CSV rather than guessing from front-fascia spacing.

## Relevant PSU socket investigation

See [`../power-supplies/C3KX-PWR-715WAC/connector.md`](../power-supplies/C3KX-PWR-715WAC/connector.md) and [connector parts index](../connectors/README.md).
