# NASA Spacewalk Analysis — Reproducible Manuscript

This repository contains a reproducible manuscript analysing six decades of NASA and Roscosmos extravehicular activity (EVA) data. Analysis figures are generated from Python and R scripts on every push to `main`, and the rendered manuscript is deployed to GitHub Pages.

[![DOI](https://sandbox.zenodo.org/badge/1217589221.svg)](https://handle.test.datacite.org/10.5072/zenodo.491791)

[![cff]([Uplo# This CITATION.cff file was generated with cffinit.
# Visit https://bit.ly/cffinit to generate yours today!

cff-version: 1.2.0
title: NASA Spacewalk Analysis
message: >-
  If you use this software, please cite it using the
  metadata from this file.
type: software
authors:
  - given-names: Luke
    family-names: B
identifiers:
  - type: doi
    value: 10.5072/zenodo.491792
keywords:
  - test
license: MIT
commit: 'no'
version: 1.0.0
ading CITATION.cff…]()


## Repository structure

```
spacewalkeRs/
├── .github/workflows/
│   └── render.yml              # Runs both scripts, renders manuscript, deploys
├── data/
│   └── data.json               # NASA EVA dataset (source: data.nasa.gov)
├── src/
│   ├── analyse_spacewalks.py   # Generates duration-based figures (Python/matplotlib)
│   └── analyse_spacewalks.R    # Generates frequency/count figures (R/ggplot2)
├── results/
│   └── figures/                # Generated on push — not committed to the repo
├── manuscript.qmd              # Pure-markdown Quarto manuscript; embeds figures
├── requirements.txt            # Python dependencies
├── DESCRIPTION                 # R package dependencies (used by CI)
├── renv.lock                   # Locked R package versions
├── references.bib              # Bibliography
├── .gitignore
└── README.md
```

## Running locally

### Python figures

Install dependencies:

```bash
pip install -r requirements.txt
```

Run the analysis script from the repository root:

```bash
python src/analyse_spacewalks.py
```

Figures are saved to `results/figures/`.

### R figures

Restore the package library using renv (first time only):

```r
install.packages("renv")
renv::restore()
```

Run the analysis script from the repository root:

```bash
Rscript src/analyse_spacewalks.R
```

Figures are saved to `results/figures/`.

### Render the manuscript

Once figures have been generated:

```bash
quarto render manuscript.qmd
```

---

## Data

The dataset (`data/data.json`) contains one record per EVA with the following fields:

| Field | Description |
|---|---|
| `eva` | EVA number |
| `date` | Date of the EVA |
| `country` | Country (`USA` or `Russia`) |
| `crew` | Semicolon-delimited crew member names |
| `vehicle` | Spacecraft or station |
| `duration` | Duration in `H:MM` format |
| `purpose` | Brief description of the EVA objective |

Source: [NASA spacewalk database](https://data.nasa.gov/dataset/extra-vehicular-activity-eva-us-and-russia/resource/1536313f-15d8-454f-9657-a4f66407886d)
