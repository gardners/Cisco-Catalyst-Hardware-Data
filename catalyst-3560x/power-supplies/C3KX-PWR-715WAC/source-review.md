# PSU source review and unresolved evidence

Reviewed 2026-11-24. Read alongside the [contact map and source register](pinout-research.md) and [probe plan](probe-plan.md). This records the useful results of the extended search, including contradictions and access limits. It is not a record of measurements on the owner's hardware.

## Scope and evidence strength

The target specimens are Lite-On **PA-1711-1-LF REV:04** and Delta **EDPS-715AB**, sold as C3KX-PWR-715WAC. The Delta specimen's complete suffix/revision still needs recording. Searches covered those OEM strings, EDPS715AB spelling, Cisco 715 W and related 1100 W identifiers, bench/charger conversions, standby/auxiliary outputs and repair discussions, including Russian repair terminology.

There are useful independent conversion observations, but no complete 16-pin factory document and no identified, load-characterised external standby output. Searching related models is useful for hypotheses; it does not verify the target connector's functions.

| Source | Material actually inspected | Useful evidence | Limit |
|---|---|---|---|
| R1, Petrakis | Public model description, labelled module photograph, connector photograph and numbered turn-on diagram | Delta A / C3KX-PWR-715WAC V02 standalone build; diagram joins 11–12 | Author report and diagram, no per-pin electrical table or auxiliary load test |
| R2, Maarten / Lawrence | Question and both answers through public API; normal page's visible comments; voltage, short-pin and coordinate images | Related Lite-On 1100 W voltages, B3–B2 enable proposal and questioner's success confirmation | Sense and bus roles remain tentative; exact successful wiring is not completely described |
| R3, FanPhys | Author description and 151 public preview frames at two-second intervals | Physical S11–S12 bridge in a separate Delta conversion | Sampled visuals, not full-motion or audio review; no inspected standby measurement |
| R6, oreo | Entire accessible page 2 of the five-page discussion | First-hand reuse of C3KX-PWR-715WAC in bench and charger assemblies | OEM suffix and connector wiring absent; remaining pages inaccessible through normal web tool |
| R7, Adjal | All three public repair posts, owner photographs and reply attachments | Delta B ground annotations and internal 12 V / 3 V observation | Main output never successfully started in the report; no exported standby rating |
| R4/R5, Cisco | Installation specifications and compatibility guidance | Main rating, LED meanings and stated replacement-family compatibility | No 16-contact assignment or external standby-current specification |

`INFERRED` in the worksheet means a research hypothesis. It is not a confidence score or a substitute for measurement. Ten of the sixteen functions remain unknown, and no electrical assignment is locally `MEASURED`.

## What the video adds

The inspected R3 storyboards cover approximately 0–300 seconds. At **202–212 seconds**, the connector close-up shows left red/right black power wiring and a bridge across the **third row's two rightmost signals**, S11–S12 in this archive. At approximately 208–212 seconds, the author's overlay highlights that same pair. See the [timestamped original](https://www.youtube.com/watch?v=h07NQ-fHocA&t=202).

This is useful corroboration of R1's drawn connection from a different builder. It establishes what was connected in the visible conversion, without identifying the endpoints' internal circuitry. Wire colour supports a polarity interpretation but is not a measurement. Other preview frames show mechanical work and assembly with the RD6018; they do not resolve an external standby rail.

The timed-text request returned an empty file. No transcript, audio or video comments were read, and short events between sampled frames could have been missed. Those gaps remain in the [retrieval queue](download-queue.md).

## What the repair report changes

R7's original owner labels **S10 and S12 as logic grounds**, marks **S07 and S11 short**, and points approximately **3 V at S11**. The ground-identification method is unstated. The final post reports internal **12 V standby and 3 V logic**, while the main converter does not start. There is no pin-specific 12 V measurement, load rating or successful repair. The title identifies Delta suffix B; the owner's suggested Cisco family is not confirmed by an inspected Cisco PID label.

The reply proposes adding load, but no successful result follows. Consequently, this thread does not establish a minimum-load requirement, a diagnosed failed component or a working cure for the pulsing fan.

The reply's two jumper attachments are duplicate screenshots from **R3's video**. They are not independent replication of the jumper procedure. The owner's annotated photograph and failure observations are the new evidence.

## Provenance: avoid counting reposts as experiments

- **R1 → 3D GO:** the index reproduces the Makerworld build. It helped locate the original and adds no independent electrical observation.
- **Possible older R1 origin:** an indexed [Thingiverse project, 4769942](https://www.thingiverse.com/thing:4769942), credited to PetrosGR on 2021-02-21, points to [Petros Projects' RD6012/DPS5015 build](https://petrosprojects.blogspot.com/2021/02/diy-bech-power-supply-based-on-rd6012.html). The [2021 seller repost](https://budgetlightforum.com/t/rd6018-rd6018w-60v-18a-power-supply-is-published/63692?page=10), post 196, independently locates that historical project link, but is not another builder's test. The original blog and Thingiverse content could not be read; common provenance with R1 remains a lead, not an established attribution.
- **R3 → R7 reply:** the public reply embeds the same FanPhys video and uses its screenshots. Only the repair owner's own observations add independent evidence.
- **R2 → RCGroups:** following the actual linked post reveals a **Dell L1100A-S0 / Lite-On PS-2212, 12 V** supply. Its connector and pin numbers do not identify the Cisco 56 V interface.

## Other references read and why they do not fill pins

| Reference | Result of review |
|---|---|
| [esk8 charger discussion, October–December 2020](https://forum.esk8.news/t/charger-from-server-power-supply/40869) | Nine public posts read. Discussion of charger suitability and possible voltage adjustment; no demonstrated connector map or auxiliary load test. The opening approximate 55 V / 6 A description is insufficient to identify an OEM variant. |
| [Cisco Community failure discussion, April 2015](https://community.cisco.com/t5/switching/switching-power-supply-damage/td-p/2614874) | Three public posts read. Several failures reported; replies suggest checking input quality. No component diagnosis, circuit tracing or pin assignments. A failure count does not establish a common repair. |
| [check_nwc_health issue 56, January 2016](https://github.com/lausser/check_nwc_health/issues/56) | Visible issue body and CLI/SNMP comparison read. Software reports a faulty supply while IOS reports the C3KX modules healthy. No circuit evidence or visible repair resolution; do not interpret a monitoring label as a diagnosed PSU failure. |
| [Cisco-hosted Delta certificate](https://www.cisco.com/web/dofc/11333024.pdf) | Lists EDPS-715AB XX and −56 V / 12.8 A, 715 W maximum. No standby-contact rating. The document's certificate validity ended in 2025; it is historical rating evidence, not a claim of current certification. |
| [ShopJimmy Lite-On listing](https://www.shopjimmy.com/lite-on-pa-1711-1-lf-715w-power-supply/) and [Delta listing](https://www.shopjimmy.com/delta-edps-715ab-715w-switching-power-supply/) | Search/page text advertises a repair video, but no actual tutorial content or video identifier was exposed in the readable Lite-On page. Queue raw HTML to check whether the badge corresponds to a real model-specific video. Do not count the badge as a repair source. |
| [TechPowerUp discussion linked by R2](https://www.techpowerup.com/forums/threads/how-to-turn-on-power-supply.147023/) | Repeated normal-web timeout. R2 quotes general suggestions from it, but the original thread has not been read. Queued with lower priority; no pin assignments adopted. |

R6 contains advice about modifying **HP** supply case connections and capacitors. That is not Cisco evidence and is not adopted. Later references to an explosion, a 5 V regulator and standby consumption concern the author's **DIY inverter**, not an EDPS-715AB auxiliary circuit. Reading the surrounding posts prevents those keywords becoming false PSU evidence.

Retail searches also produced mismatched generic ATX connector/specification tables and references to other Cisco families. No retailer's uncorroborated 12 V / 3.3 V claim is used to fill this connector map. A **PA-1711-1A-LF**, later PWR-C1 model or unrelated Delta supply needs its own identity and evidence; a similar name is insufficient.

## Questions that the next measurements can discriminate

| Open question | Most informative observation | What would still remain unknown |
|---|---|---|
| Are S10/S12 the same return on each specimen? | Unpowered resistance between them and to both blades/case, with polarity and settling recorded; then referenced voltages | Whether a measured connection is a direct return, sense path or another circuit unless corroborated |
| Is S12 low-side sense or a logic return? | Compare its resistance/voltage relationship to both power rails and S10 separately by OEM | A universal role across revisions |
| Is any unknown high contact a power output? | Established return, complete idle survey, light-load response, then unpowered motherboard trace | Ampere-level rating after only a light test |
| Is internal 12 V available externally? | All 16 contacts surveyed in AC-only and normal-running states | Whether an absent voltage is internal-only, state-dependent or variant-dependent |
| Are S09/S14 clock and data? | Passive normal-operation waveform capture with verified reference and logic levels | PMBus/SMBus command set, addresses and permissible writes |
| What does S07 do? | Confirm staggered length and trace/capture its normal operation | Presence, inhibit or other role from length alone |

These observations are prioritised in [probe-plan.md](probe-plan.md). A useful first session can stop after returns, idle voltages and the three light-load candidates; the research does not require opening the mains enclosure.

## Repository and access handling

Only original summaries, factual transcriptions, templates and the archive's original SVG are added. No third-party photos, screenshots, models, PDFs, transcripts, HTML or API dumps are included. Source assets inspected during research were kept under `/tmp` and are not durable archive dependencies.

After the owner's instruction to queue curl-dependent work, no further curl permissions were requested. Ordinary web tools were used; incomplete sources are queued with their exact URLs and the question each download could answer. Inaccessible material is not represented as reviewed. The original user hardware remains unmeasured.
