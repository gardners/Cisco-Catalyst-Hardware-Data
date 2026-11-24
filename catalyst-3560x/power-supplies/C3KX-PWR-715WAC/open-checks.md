# Unresolved power-supply questions

- Identify original PCB connector and actual mating part through marking, manufacturer drawing and physical trial.
- Register each specimen to the fan-right module-face reference in [pinout-research.md](pinout-research.md), including complete OEM/revision labels and short-contact positions.
- Verify the proposed left/high and right/low power-contact assignment and the relationship of both rails to chassis/earth. [M1](measurements/2026-11-25-case-bond.md) records a case/earth bond and no case-to-blade continuity beep on one unidentified specimen, not resistance measurements. Check both OEMs in resistance mode and retain specimen identity and test conditions before concluding either output floats.
- Follow [probe-plan.md](probe-plan.md) priorities 0–3 to investigate an external standby supply: establish the return first, then measure S04/S15/S03 unloaded and under small resistor loads. Treat 12/5/3.3 V at 0.5–1.5 A as an unsourced lead; do not assign a current rating from idle voltage or a 1 mA test.
- Test whether the repair report's internal 12 V standby circuit is exported at all. Complete all 16 voltage readings; the report gives no 12 V contact or current capability.
- Resolve the reported S11–S12 Delta enable connection versus S11–S10 on the related Lite-On 1100 W unit; do not assume S10 and S12 are interchangeable returns.
- Check the Delta repair owner's S10/S12 logic-ground annotations against actual resistance paths; retain the competing S12 remote-sense hypothesis separately by variant.
- Test the S08/S12 remote-sense and S09/S14 I²C hypotheses separately on Lite-On PA-1711-1-LF REV:04 and Delta EDPS-715AB specimens.
- Identify S01–S07, S13, S15 and S16; the related 1100 W idle voltages do not establish their functions. In particular, S07's reported shorter contact does not identify an interlock.
- Register both socket bodies and board-locks against H07/H08; candidate absolute X placement and local edge intersection remain estimates.
- Determine correct PCB tail drill diameters, hole plating, copper land sizes and keying.
- Measure variant-specific module behaviour for Lite-On and Delta separately.

The external source register, all 16 reference voltage readings, and a sequence for collecting local evidence are in [pinout-research.md](pinout-research.md). No third-party source images are included in the archive.

For outstanding documentary work, see the [source review](source-review.md) and [prioritised download queue](download-queue.md).
