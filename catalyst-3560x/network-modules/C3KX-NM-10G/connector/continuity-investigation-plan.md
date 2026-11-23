# Unpowered continuity investigation — prioritised bench protocol

**Safety:** Disconnect switch mains, remove both PSU modules, confirm all rails discharged, and never probe powered high-speed contacts with ordinary DMM probes. For mated tests, insert fully with mechanical guides intact; do not hot-plug while test leads are attached. Mating may connect blade power contacts even though no supply is present. Do not short neighboring 1.4 mm pitch holes using large probes. Label all probe polarity and resistance values. Do not infer electrical continuity through capacitors.

The following measurements make sense in escalating order; the aim is *high information gained per probe*, not exhaustively ringing 192 contacts without a hypothesis.

## Session A — register grounds and key orientation (host board only)

| Rank | Probe A | Probe B | Useful outcome |
|---|---|---|---|
| A1 | TP78 | TP81 | Confirm both silk-labelled points on same ground plane |
| A2 | TP81 | photo grid R01C01 through R12C16 | Mark direct-ground contacts as CONFIRMED; group by column and compare with TE 64-GND population |
| A3 | TP81 | all eight large blade-hole groups | Distinguish grounds, rails and shields. Keep power blade net map separate from signal grid |
| A4 | TE A1/keying physical housing | photo corner R01C01 | Establish TE row lettering and left/right orientation from manufacturer's *component-side* drawing, with photos |

**Fast discriminating probes:** See [two-phase ground hypothesis](tinman-two-phase-ground-HYPOTHESIS.csv). Probe `R01C01`, `R03C01`, `R01C02`, `R03C02` against TP81 first. This tests the candidate `SSG` vs `GSS` stagger phase, but both candidates remain unconfirmed until repeated over multiple columns.

**Efficiency:** Once a full column's ground positions are established, test corresponding alternating-column positions. TE's routing guide specifically describes staggered ground placement; do not assume uniform positions.

## Session B — serial-network component classification

| Rank | Measurements | Interpretation |
|---|---|---|
| B1 | One side of each candidate C590-C600 capacitor -> TP81 | One side GND suggests decoupling, two floating sides supports series AC coupling (not proof) |
| B2 | For two adjacent caps suspected to form a pair, pad A -> closest contact photo ID; repeat pad B | Two separate conductors with same routing and nearby ground is a plausible differential pair |
| B3 | Repeat for C665-C674 and C706-C713 | Build candidate functional groups; record every cap designator and both pads separately |
| B4 | Continuity on same cap with probes across both terminals | Should read open/charge on most DC-blocking AC coupling components; a low-ohm reading may indicate shunt/parallel circuit |

Record results as `part`, `pad`, `photo_contact_id`, `ohms`, `beep`, `signal_hypothesis`, `evidence`, not only the end result.

## Session C — sled alone, unpowered

1. Photograph readable legends of small ICs next to BCM8727 and the four cages. Compile a component register first.
2. On accessible vias/coupling capacitors by BCM, measure direct continuity to signal contact tails/terminations accessible on sled underside. A BCM BGA ball cannot be probed directly while fitted.
3. Check each SFP cage's **high-speed TD±/RD± connections** to adjacent capacitors or vias, tracking which two cages route to the BCM. Check copper cage shield separately from circuit GND.
4. Trace obvious regulator outputs and brownout/reset connections; don't assume a single 3.3V rail.
5. For clocking, determine whether the sled carries a clock oscillator; no powered test until supply sequencing and current limiting are known.

## Session D — both PCBs mated, unpowered

1. Verify signal identity via easily reached host-grid holes to accessible sled-side signal-tail vias/testpoints. Record directions **without assuming left-right correspondence**.
2. Start with **one** suspected capacitor pair: host capacitor pad and sled-side capacitor pad, then search for a low-ohm path. A link that only appears through a capacitor is *not* a valid DC continuity result.
3. Determine whether the four photo-grid corners map to reversed x/y axes on sled. This establishes complete physical contact-ID conversion, which can then be applied to the TE contact name table.
4. Confirm GND on both boards, then any blade rail groups; ensure not confusing mechanical guide pins, shields and contacts.

## Later destructive work, if necessary

See the [BCM8727 candidate ball targets CSV](BCM8727-priority-BGA-lands-for-later-probing.csv) for all 32 XAUI pins, clock pins and management pins from the independent Terasic-based register. A cheap sacrificial C3KX-NM-10G with its **BCM8727 BGA removed** would expose chip land patterns for a full wire-by-wire route map. Use known BCM ball names from the Terasic 324-ball reference and probe exposed *PCB lands* against accessible connector contacts/vias. This avoids guessing through hidden layers. But: BGA lift risks torn pads and damaged vias; flux residue may conceal lands; many XAUI paths have **series AC caps**, so test *each side* or map on the appropriate side; pad numbering/orientation must be verified; **known Terasic assignments may be revision-specific**. A controlled rework oven/hot-air station, preheater and microscope/needle probes are preferable. This is a later-stage, sacrificial-board technique, **not necessary for first-pass ground/coupling discovery**.

## Probe log

Use [probe-log-template.csv](probe-log-template.csv), with *each measurement separate* and explicit `UNCERTAIN` status. Do not promote a hypothesis to a confirmed Cisco net until both endpoints are physically measured.
