# Analysis plan

This is the proposed workflow for the post-fire annual herbaceous cover question. Nothing here is locked — please edit it, push back on the framing, or open an issue if you want to change the direction.

## Research question

**Main:** Do burned areas in the Great Basin show greater post-fire increases in annual herbaceous cover than comparable unburned areas nearby?

**Secondary:** How does the post-fire response vary by fire year, fire size, and location within the Great Basin?

## Why annual herbaceous cover, and not cheatgrass directly

Worth flagging so we're aligned on the framing before we start producing numbers:

- **RCMAP annual herbaceous cover** is the main response variable. It's a continuous annual time series (1985–present, 30 m), which is what a pre/post-fire comparison needs.
- Published work on post-fire Great Basin rangelands consistently finds that annual herbaceous cover in recently burned sites is dominated by invasive annual grasses, with cheatgrass (*Bromus tectorum*) as the dominant contributor. So RCMAP annual herbaceous cover is a defensible **proxy for invasive annual grass expansion**.
- The **USGS predicted-cheatgrass rasters** (Pastick / Boyte) I mentioned earlier *are* cheatgrass-specific, but they're a **single static prediction surface** published with low / medium / high uncertainty quantiles — not a time series. We **cannot** use them for pre- vs post-fire comparison.
- Where the cheatgrass raster *does* help is as a **supplemental context layer** — e.g. asking whether the post-fire response in RCMAP is larger in areas predicted to be cheatgrass-prone. That lets us tie the annual herbaceous story to cheatgrass without overclaiming what the data actually measure.

Language convention for the writeup: say **annual herbaceous cover** and **invasive annual grass expansion** where RCMAP is doing the work, and only say **cheatgrass** when we're specifically invoking the predicted-cheatgrass raster as a context layer.

## Study area and datasets

- Study area is strictly inside the Great Basin boundary polygon already in the repo.
- **MTBS** tells us where and when fire occurred.
- **RCMAP annual herbaceous cover** is the pre/post response variable.
- **USGS predicted cheatgrass (Pastick / Boyte)** is supplemental context only — never used as a pre/post measurement.

## Proposed workflow

### Phase 1 — Data prep (open)
- [ ] Confirm RCMAP rasters clip cleanly to the Great Basin polygon
- [ ] Confirm MTBS perimeters are filtered to fires inside the Great Basin
- [ ] Decide the eligible ignition-year range given RCMAP temporal coverage

### Phase 2 — Burned-area summary (open)
- [ ] Extract mean RCMAP annual herbaceous cover inside each fire perimeter, pre- and post-fire
- [ ] Decide pre/post window length (1-year vs multi-year mean)
- [ ] Summarize direction and magnitude of change across fires

### Phase 3 — Burned vs unburned (open)
- [ ] Define unburned control polygons (e.g. local ring buffer outside the fire, same year, same Great Basin)
- [ ] Extract matched RCMAP means in the controls
- [ ] Compare burned change vs control change (paired tests)

### Phase 4 — Stratification (open)
- [ ] By ignition year
- [ ] By fire size class
- [ ] By fire severity (dNBR, if available in MTBS)

### Phase 5 — Robustness and context (open)
- [ ] Sensitivity to control-buffer distance
- [ ] Bootstrap confidence intervals for the fire-attributable effect
- [ ] Supplemental cheatgrass overlay — static predicted-cheatgrass raster used only for context stratification, not pre/post

### Phase 6 — Write-up
- [ ] Maps (study area, fire locations)
- [ ] Results figures
- [ ] Limitations and scope of inference (including: RCMAP ≠ cheatgrass-only, cheatgrass raster is static)

## Open questions we should decide together

- What pre/post window length best balances signal vs sample size — 1 year either side, or multi-year means?
- How should unburned controls be matched — local ring buffer, random draw inside the basin, or some kind of environmental matching?
- Do we restrict the analysis to a specific ecoregion inside the Great Basin, or treat the whole basin as one?
- How do we want to present the cheatgrass supplemental analysis — as a short context section, or as a separate figure?

## Datasets at a glance

See `DATA_SOURCES.md` for full metadata. Briefly:

- **MTBS** fire perimeters — 1984 to present
- **RCMAP** annual herbaceous cover — 1985 to present (we have 2012–2020 clipped locally)
- **Great Basin boundary** — committed to the repo
- **USGS predicted cheatgrass** (Pastick / Boyte) — static prediction, supplemental use only
