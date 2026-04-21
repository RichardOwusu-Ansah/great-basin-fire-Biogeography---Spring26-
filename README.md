# Post-fire Annual Herbaceous Cover in the Great Basin

Hey team — this is our shared repo for the class project. The question we're working on:

> Do burned areas in the Great Basin show greater post-fire increases in annual herbaceous cover than comparable unburned areas nearby?

I've set up the repo so we can all start from the same place. The working notebook (`great_basin_work.ipynb`) loads the datasets and walks through one fire as a worked example, so you can run it end-to-end on your machine before we split up the next steps.

Please read `ANALYSIS_PLAN.md` — it lays out the proposed workflow and the open questions we still need to decide together.

---

## A note on the response variable

We're using **RCMAP annual herbaceous cover** as the main response variable, not a cheatgrass-specific layer. A few reasons, worth flagging up front so we're all on the same page:

- RCMAP gives us a continuous annual time series (1985–present, 30 m), which is what we need for a pre/post-fire comparison.
- Published work on post-fire Great Basin vegetation consistently finds that annual herbaceous cover in recently burned rangelands is dominated by invasive annual grasses, with cheatgrass (*Bromus tectorum*) as the dominant contributor. So treating annual herbaceous cover as a **proxy for invasive annual grass expansion** is defensible.
- I looked into the USGS predicted-cheatgrass rasters (Pastick / Boyte) that I flagged earlier. They're real cheatgrass-specific data, but they are **not** a time series — they're a single static prediction surface published with low / medium / high uncertainty quantiles. That means we **cannot** use them for a pre- vs post-fire comparison.
- What we *can* do with the cheatgrass raster is use it as a **supplemental context layer** — for example, to check whether the post-fire annual herbaceous response is consistent with areas predicted to be cheatgrass-prone. That keeps the cheatgrass framing honest without overclaiming.

Bottom line on wording: we should say "annual herbaceous cover" and "invasive annual grass expansion" where the data support it, and only say "cheatgrass" when we're specifically using the cheatgrass-specific raster as context.

---

## Repository layout

```
├── great_basin_work.ipynb   Shared working notebook (data loading + worked example)
├── data/
│   ├── raw/
│   │   └── boundaries/      Great Basin study-area polygon (committed)
│   │   (mtbs/, rcmap/, cheatgrass/ are downloaded locally — see Data setup)
│   └── processed/           Outputs of local preprocessing (not committed)
├── DATA_SOURCES.md          Dataset catalog
├── ANALYSIS_PLAN.md         Proposed workflow and open questions
└── requirements.txt         Python dependencies
```

---

## Setup

### 1. Python environment

Requires **Python 3.10+**.

```bash
python -m venv .venv
source .venv/bin/activate        # macOS / Linux
pip install -r requirements.txt
```

### 2. Data setup

The rasters and fire perimeters are too large for Git and aren't committed. Please download them into your local `data/raw/` folder.

| Dataset | Source | Save to |
| --- | --- | --- |
| Great Basin boundary | already in the repo | `data/raw/boundaries/` |
| MTBS fire perimeters | [MTBS direct download](https://www.mtbs.gov/direct-download) | `data/raw/mtbs/` |
| RCMAP annual herbaceous (2012–2020) | [MRLC RCMAP portal](https://www.mrlc.gov/data?f%5B0%5D=category%3ARCMAP) | `data/raw/rcmap/` |
| USGS predicted cheatgrass (supplemental only) | [ScienceBase DOI:10.5066/P9OEY7X5](https://doi.org/10.5066/P9OEY7X5) | `data/raw/cheatgrass/` |

See `DATA_SOURCES.md` for full metadata.

---

## Working notebook

Open `great_basin_work.ipynb` in VS Code or JupyterLab:

```bash
jupyter lab great_basin_work.ipynb
```

The notebook:

1. Loads the Great Basin boundary, MTBS fire perimeters, and RCMAP annual herbaceous rasters
2. Filters MTBS to fires inside the Great Basin
3. Walks through one fire as a worked example: clip RCMAP to the perimeter and compute mean pre- and post-fire annual herbaceous cover

It's meant as a starting point — just so we all have the same data loading pattern and a sanity-check example. The real work is in `ANALYSIS_PLAN.md`.

---

## How we'll work

- Pull the repo and get the environment running
- Run the notebook end-to-end to make sure the data loads on your machine
- Pick a task from `ANALYSIS_PLAN.md` (or propose one) and open an issue so we don't step on each other
- Branch, work, open a PR, review
