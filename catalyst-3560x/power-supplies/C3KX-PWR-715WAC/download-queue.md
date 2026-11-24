# PSU research retrieval queue

Prepared 2026-11-24 for the owner's return. **No action is needed while away.** These are remaining source gaps after ordinary web access, not requests for new permissions. The current findings and access limits are recorded in [source-review.md](source-review.md).

Download third-party source material to a directory **outside the repository**, for example `/tmp/cisco-psu-followup/`. Do not commit the downloads, even if they are publicly readable. The repository should receive our own observations and links; redistribution would require separately established rights.

The [CSV queue](download-queue.csv) contains exact URLs, proposed basenames and the question to resolve. Priority 1 is directly relevant to standby or original pinout evidence; priority 2 may add background. Some queued requests may still need a normal browser or may return no useful content.

## Priority 1

1. **Original Petros Projects build and comments:** [February 2021 RD6012/DPS5015 post](https://petrosprojects.blogspot.com/2021/02/diy-bech-power-supply-based-on-rd6012.html). Ordinary web access reached Google's access-interruption page, so the article and comments were not read. The indexed Thingiverse description links here. Look for connector wiring, standby/current reports, source attribution and replies explaining the fan or enable behaviour. Preserve the `bech` spelling in the URL.
2. **Original Thingiverse project and comments:** [thing 4769942](https://www.thingiverse.com/thing:4769942). Normal access failed. The historical seller repost credits PetrosGR, 2021-02-21. Determine whether this is R1's earlier publication and whether comments add measurements; do not count a repost as a second experiment.
3. **FanPhys audio, transcript and comments:** [original video](https://www.youtube.com/watch?v=h07NQ-fHocA). Description and sampled frames have already been reviewed, including the S11–S12 bridge at 202–212 s. A caption request returned no content. The missing material could explain the fan wiring, any minimum-load condition or auxiliary power use. A curl of the watch page saves HTML, **not the video or a transcript**; obtain those separately through an available browser/download facility. Do not assume the English automatic-caption track can be retrieved at a stable signed URL.
4. **Complete Stack Exchange comments:** [question comments API](https://api.stackexchange.com/2.3/questions/476293/comments?site=electronics&filter=withbody&pagesize=100), [Lawrence answer comments](https://api.stackexchange.com/2.3/answers/476626/comments?site=electronics&filter=withbody&pagesize=100), and [Müller answer comments](https://api.stackexchange.com/2.3/answers/476303/comments?site=electronics&filter=withbody&pagesize=100). The normal page exposes the startup confirmation and A.K.'s standby hypothesis, but hides additional discussion under the second answer. API access failed through the web tool. Look for follow-up measurements, actual successful wiring or the origin of a standby-current claim. Inspect `has_more`; this page-size choice does not guarantee completeness.
5. **Related Lite-On 1100 W label and internal photographs:** [label](https://i.sstatic.net/BNepe.jpg), [internal photo 1](https://i.sstatic.net/vYRuM.jpg), [internal photo 2](https://i.sstatic.net/YXeX0.jpg), [internal photo 3](https://i.sstatic.net/XpPb8.jpg). The connector, voltage and short-contact images are already inspected. These remaining images might establish the exact OEM model and reveal readable control-board/connector traces. They cannot by themselves verify a 715 W pinout or current rating. Download only these still-uninspected originals, not copies of already-reviewed assets.

## Priority 2

6. **ShopJimmy raw listing HTML:** [Lite-On](https://www.shopjimmy.com/lite-on-pa-1711-1-lf-715w-power-supply/) and [Delta](https://www.shopjimmy.com/delta-edps-715ab-715w-switching-power-supply/). Both expose a repair-video badge in search/page text; no actual tutorial was identified. Check HTML for a real embedded video ID and exact model match before spending time on the supposed tutorial. The badge may be generic page furniture.
7. **Remaining BackShed thread pages:** [page 1](https://www.thebackshed.com/forum/ViewTopic_mobile.php?P=1&TID=16960), [page 3](https://www.thebackshed.com/forum/ViewTopic_mobile.php?P=3&TID=16960), [page 4](https://www.thebackshed.com/forum/ViewTopic_mobile.php?P=4&TID=16960), [page 5](https://www.thebackshed.com/forum/ViewTopic_mobile.php?P=5&TID=16960). Page 2 was fully read and describes reuse, but no pinout. Check remaining pages for Cisco-specific details. Keep HP grounding changes and DIY inverter repair/standby discussion separate from Cisco evidence.
8. **TechPowerUp original thread:** [How to turn on power supply](https://www.techpowerup.com/forums/threads/how-to-turn-on-power-supply.147023/). Repeated normal-tool timeouts. It is a general-method reference linked by the 1100 W question; inspect the actual PSU identity before treating any advice as relevant. Lower priority than original target-family evidence.

## Example fetch for when convenient

The following is an example for the owner to run later; it has **not** been run as part of this queue. The CSV is a manifest, not an automatically executed download script.

```sh
mkdir -p /tmp/cisco-psu-followup
curl --fail --location --retry 2 --connect-timeout 15 --max-time 120 \
  --output /tmp/cisco-psu-followup/petros-2021-build.html \
  'https://petrosprojects.blogspot.com/2021/02/diy-bech-power-supply-based-on-rd6012.html'
```

For each result, record retrieval time, final URL, HTTP outcome and whether it is actual content or an error/login page. A successful HTTP status alone does not mean the article, comments or video were retrieved. Respect login restrictions; there is no need to access private material to continue the investigation.

Once retrieved, review for the specific question in the manifest, update the source register with what was actually inspected, and retain all local electrical assignments as unverified until the specimens are probed.
