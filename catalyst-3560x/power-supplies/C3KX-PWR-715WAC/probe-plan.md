# Prioritised PSU connector probing plan

Prepared 2026-11-24 for the **Lite-On PA-1711-1-LF REV:04** and **Delta EDPS-715AB** specimens. Use the related Lite-On 1100 W report as a guide to where to look, not as a verified pinout. Source IDs and the physical reference are in [pinout-research.md](pinout-research.md).

**First objective:** identify the electrical reference and find whether a connector contact supplies usable low-voltage power with the main output disabled. The reported **12 / 5 / 3.3 V at 0.5–1.5 A** is an investigation lead; neither the voltage, contact nor current rating has been established for these specimens.

A Delta `EDPS-715AB B` repair owner reports **internal 12 V standby and 3 V logic** [R7], without identifying an exported power contact or current rating. Their connector photograph marks **S10 and S12 as logic grounds**, with the measurement method unspecified. This makes checking those returns especially valuable; it does not justify putting a 12 V load on any signal pin.

The highest-value first session is priorities 0–3 below. It can produce useful results without enabling the 56 V output. Keep the two OEM variants separate throughout.

## Equipment and recording

- Floating handheld DMM; insulated fine probes or securely retained test leads; insulating support for the module. The closed PSU case and its protective-earth connection stay intact.
- A physically secure way to access contacts without bridging neighbours. The proposed Amphenol mate has not been trial-fitted: do not force it or rely on its nominal numbering.
- For the low-current tests: 47 kΩ, 10 kΩ and 3.3 kΩ resistors. Ordinary 0.25 W parts suffice **for the confirmed 3.3 V test case** below. Use measured resistance values in calculations.
- [Connector readings template](probe-readings-template.csv): one row per contact and OEM specimen, with the 1100 W reference voltage in a distinctly named comparison column.
- [Standby load-test template](standby-load-tests-template.csv): prefilled with the three first-pass contacts and the three resistors for each specimen. All actual measurement fields are blank. Its resistor values apply only after a candidate is established to be near 3.3 V.

Record date, instrument, full PID/VID, OEM suffix/revision and a unique specimen ID. Blank means **not measured**. Record `OL`, a changing reading or a signed voltage explicitly; do not turn them into zero. Record the meter polarity for resistance readings; the template assumes black/COM on the named reference and red on the contact unless noted otherwise.

Use the DMM's **voltage mode** across outputs; estimate load current from a known resistor. An ammeter placed directly across a rail is a short circuit. Disconnect AC before placing or moving clips, resistors or jumpers, and verify accessible contact voltages have decayed before resistance measurements. Keep the mains enclosure closed. Do not earth a DC contact, connect USB-grounded instruments, or attach an oscilloscope ground clip while the DC reference is unresolved.

## 0 — Fix orientation and specimen identity

**No AC connected.** Photograph the label and connector. Look into the PSU's DC mating face, **fan right**, broad sheet-metal wall above and folded housing seam below:

```text
                    top
 Left blade     S01  S02  S03  S04     Right blade
                S05  S06  S07  S08                    FAN -->
                S09  S10  S11  S12
                S13  S14  S15  S16
                    seam
```

Check the photo against the [reference drawing](figures/signal-contact-map.svg). Do S07 and S11 appear shorter on this specimen, as in the related 1100 W photograph? Record the answer without assigning an interlock function. `POWER_BLADE_A` means left; `POWER_BLADE_B` means right. These are archive IDs, not connector-vendor numbers.

**Deliverable:** one labelled photograph and specimen identity per OEM variant. If the physical arrangement differs, resolve that before transferring any source pin references.

## 1 — Find return paths with the supply unpowered

With AC disconnected and accessible DC contacts discharged, measure resistance from both power contacts to the metal case, then from each signal contact to:

1. Left power contact.
2. Right power contact.
3. Metal case / protective earth.

**Measure S10 and S12 first**, followed by S04, S15 and S03. Then complete the remaining contacts. Also measure left-to-right power-contact resistance and S10-to-S12 resistance; record these in the notes. Note readings that change while capacitors charge from the meter. For ambiguous paths, repeat with reversed meter polarity and record both results.

The first question is whether S10 is a direct return to either blade or the case, and whether S12 is the same net or has an intervening network. This directly tests R7's two ground annotations against R2's sense hypothesis. A finite resistance to a blade may be a sense resistor, protection path or other circuitry. A continuity beep alone is insufficient to call it ground. Even a case bond must be recorded rather than inferred from Cisco's negative-voltage convention.

If S03/S04/S15 are accessible, also check their pairwise resistance and resistance to the tentative S09/S14 signal contacts. Direct continuity versus a resistive path may help separate a shared rail from signals pulled up to it. Equal unloaded voltage does not establish a shared net.

**Deliverable:** unpowered resistance columns, especially the relationships of S10 and S12. If no reference can be identified, retain the left/right/case measurement system; do not invent a logic-ground connection for a load test.

## 2 — Record AC-only voltages without enable links

Arrange retained voltage-test leads with AC disconnected, clear the output contacts of loose conductors, and apply AC with **no jumper or external load**. Observe the LEDs and fan. First measure the signed voltage **left blade relative to right blade**, and each blade relative to the case.

Call this state **AC-only / no jumper**, not automatically standby: if a main-output-sized voltage is already present, the module's behaviour differs from the assumed disabled state. Record it and reassess before proceeding.

Record **AC OK and PS OK separately**. Cisco's Table 5 [R4] describes AC OK green as input present; PS OK off can mean output disabled or input outside range, green means output supplied, and red means output failed. A stopped or pulsing fan alone does not identify the cause. In particular, the unsuccessful repair report does not establish that pulsing is normal or that adding a load cures it.

For each signal, record its voltage relative to the left blade. This reproduces the 1100 W source's reference. Also record voltage relative to the right blade and case, using separate power-off/reposition/power-on cycles where needed for secure access. Begin with S10 and S12, then the low-voltage candidates:

| Order | Contact | 1100 W comparison, relative to left blade | Why look here |
|---:|---|---:|---|
| 1 | S10 / B2 | 0 V | Proposed enable reference; find its actual relationship to both blades. |
| 2 | S12 / B4 | 0 V | Delta enable endpoint and owner-labelled logic ground [R7]; competing sense hypothesis [R2]. |
| 3 | S04 / D4 | 3.28 V | Unassigned high contact; useful first standby lead. |
| 4 | S15 / A3 | 3.26 V | Unassigned high contact; second standby lead. |
| 5 | S03 / D3 | 3.25 V | Unassigned high contact; third standby lead. |
| 6 | S09, S14, S11 | About 3.25–3.28 V | Possible I²C / enable signals: measure, but exclude from the initial supply-loading shortlist. |
| 7 | All other contacts | See worksheet | Complete the table, including any unexpected 5 V or 12 V readings. |

S04's slightly higher source voltage is a search heuristic, not a functional identification. The three candidate voltages are from **another module**, not acceptance limits for these specimens.

The R7 internal 12 V observation is a reason to complete the **whole connector survey**, rather than concluding that the three 3.3 V candidates are the only possibilities. If no external 12 V appears, that is consistent with an internal-only rail, a different variant, or an untested operating state; it does not by itself choose among them.

**Deliverable:** actual AC-only readings and main-output state for each OEM. Do not assume that the lower-potential main blade is logic ground: the source measured its 3.3 V signals relative to the **left** blade, and a disabled main output can conceal differences between the two blades.

## 3 — Distinguish a weak pull-up from a low-voltage supply candidate

Proceed only for a contact whose low voltage and reference have been established by priorities 1–2. Choose S04 first, then S15 and S03. Keep the main output disabled and change only one connection at a time. If the reference remains ambiguous, skip loading and pursue the unpowered motherboard trace in priority 4.

For a candidate actually measuring approximately **3.3 V**, record its unloaded voltage, then load it to its established return in this order. Disconnect AC to fit or change each resistor.

| Resistor | Approximate current at 3.3 V | Resistor power at 3.3 V | Purpose |
|---:|---:|---:|---|
| 47 kΩ | 70 µA | 0.23 mW | Initial check for a very weak source. |
| 10 kΩ | 330 µA | 1.1 mW | Useful discriminator for a kilohm-scale pull-up. |
| 3.3 kΩ | 1 mA | 3.3 mW | Only if the earlier readings remain stable. |

Record loaded voltage, LED/fan changes and whether any other contact or main-output state changes. If voltage falls by roughly **10% or more**, or operation changes, remove the load and stop that candidate's sequence. This is a conservative investigation stop criterion, not a claimed regulation specification. A status or enable input can change system behaviour under even a light load.

For a **5 V or 12 V** candidate, do not use the prefilled resistor sequence unchanged. Select resistors for comparable small currents using `R = V / I`, and check dissipation with `P = V² / R`. Examples for a final approximately 1 mA check are 5.1 kΩ at 5 V and 12 kΩ at 12 V. Record the substituted resistance and establish the correct return first.

Calculate actual current as `I = V_loaded / R_load`. A rough static source resistance is `R_source ≈ R_load × (V_unloaded / V_loaded − 1)`, assuming a stable source; it does not identify the circuitry by itself. A 4.7 kΩ pull-up to 3.3 V would produce only about 2.24 V into 10 kΩ. This is an illustrative divider calculation, not a measurement on these supplies.

**Interpretation:** significant sag suggests a weak signal pull-up or another current-limited source. A steady voltage at 1 mA establishes only that the contact supplied that tested load in that state. A driven logic output could also pass this test. It does **not** establish an externally intended standby rail or a 0.5–1.5 A capability.

**Deliverable:** one voltage-versus-load record per candidate, and a shortlist labelled weak source, stiff candidate at tested current, or unresolved. This is a useful stopping point for the first session.

## 4 — Corroborate the standby rail before substantial loading

On the **unpowered original motherboard**, follow the corresponding socket contacts toward low-voltage decoupling, a regulator input or an identifiable standby load. Record continuity and component markings. Keep the PSU housing closed. This can distinguish a power feed from a GPIO, sense input or serial bus without loading an unidentified pin harder.

For a contact corroborated as a power output, controlled load steps can subsequently establish useful operating points, for example 1, 5, 10, 25, 50 and 100 mA, stopping at sag, instability or abnormal heating. Choose each load from the measured voltage and verify resistor power rating; never start by demanding 0.5 A. Do not attempt these higher steps on a contact identified only by a stiff 1 mA reading.

Record current, voltage, duration, AC-only/running state and temperature behaviour at each point. A successful test establishes that operating point under those conditions, **not a manufacturer's continuous-current rating**. Testing to destruction or an unknown protection limit is not needed. The 0.5–1.5 A claim remains unverified until supported by a suitable specification or a justified, documented characterisation.

**Deliverable:** pin and return identified as a power path, with an actual tested current and state; otherwise leave current capability unknown.

## 5 — Investigate main-output enable after the reference is settled

The reports use different endpoints: two Delta 715 W conversions show **S11–S12** [R1, R3]; related Lite-On 1100 W uses **S11–S10** [R2]. R7 labels both possible endpoints as logic grounds on its Delta specimen but still reports failure to start. Do not install either as a blind short, and do not bridge S10 to S12. Remove exploratory standby loads before this phase.

If S11 has been established as a low-voltage control candidate, and one endpoint has been independently established as its control return, an initial **1 kΩ** link from S11 to that return limits the test current compared with a short. Fit it with AC disconnected, monitor S11 relative to that return and the signed main-output voltage, then apply AC. Do not use a current-limiting resistor as a substitute for verifying the reference.

Record whether S11 is actually pulled low, the LEDs, main voltage and fan behaviour, including behaviour after about a minute. Failure to enable through 1 kΩ is inconclusive: the signal may not have reached a valid low level, the assignment may differ, or another condition may be needed. Do not escalate to a direct short or lower resistance merely because it did not start. Resolve the circuit or seek additional evidence first.

If a brief output pulse occurs, record it without adding more jumpers. R2 suggests a missing sense connection could cause overvoltage shutdown, but neither that diagnosis nor a minimum-load explanation has been demonstrated on these specimens. Treat an ordinary DMM reading as potentially missing a short transient; do not attach an earth-referenced scope until its reference has been resolved.

If S12 follows the lower main-output rail while S10 follows a different reference, **do not use S12 as the return for S11**. The competing source assignments then require further investigation. Optional sense links suggested for the 1100 W module are a separate hypothesis; do not add them simultaneously with an enable test.

**Deliverable:** a per-specimen enable observation with its actual reference and resistor, or a precise reason this test was deferred.

## 6 — Classify the remaining signals using normal switch operation

If a working original switch is available, compare AC-only and running voltages, and capture S09/S14 passively after verifying logic levels and instrument grounding. Confirm clock/data roles from activity before issuing any transactions. Observe status transitions and correlate short-contact behaviour with normal insertion/control only when a suitable protected interface is available; do not simulate hot-swap by waving loose wires over powered contacts.

Record any pin's change of function or voltage between states. A signal that is high when idle is not automatically a supply. Address straps, power-good, fan control, current-share and inhibit functions remain open until supported by traces or observations.

## How to hand back the results

Save copies of the two CSV templates under specimen/session-specific names, keeping the templates blank. Include the labelled owner photos and note any departures from this plan. Even just **the unpowered S10/S12 relationships and AC-only S03/S04/S15 readings** will substantially narrow the next investigation. The full priority 3 load readings would additionally distinguish several standby candidates from weak pull-ups.
