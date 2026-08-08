# Diameter Data Challenge — Forest Mensuration

Quality audit and statistical characterization of DBH (diameter at breast height)
data for a real eucalyptus stand, developed as part of the Forest Mensuration
graduate course.

## Context

This repository contains the analysis for the **Diameter Data Challenge**, using
`inventario.xlsx` — a real forest inventory dataset (215 trees, 6 sample plots,
7-year-old eucalyptus stand, clone 1501, 3×3 m spacing, reform regime).

Full assignment brief: [`docs/Desafio_diametro.pdf`](docs/Desafio_diametro.pdf)

## Objectives

The forestry manager requested answers to six questions before the diameter data
is used in the official inventory report:

1. Descriptive statistics of DBH (arithmetic mean, quadratic mean, standard
   deviation, min/max, coefficient of variation) — per plot and for the whole stand
2. Diameter class distribution (Sturges' rule) and an estimate of trees with
   DBH ≥ 15 cm across the full 48.7 ha field
3. Basal area (m²) and basal area per hectare (m²/ha) — per plot and total
4. A data quality audit — statistical criteria for identifying suspicious DBH values
5. DBH histograms (per plot and for the whole stand), with interpretation
6. Estimated plot area and trees/ha, deduced from the 3×3 m spacing

## Methodology summary

- **Outlier detection:** Interquartile Range (IQR) criterion, applied per plot
  (more robust than z-score given the small sample size per plot, n = 32–41)
- **Diameter classes:** class width = standard deviation of the group (plot or
  stand); number of classes = range (max − min) ÷ standard deviation, rounded up.
  Applied separately to each plot's own data and to the stand as a whole, per the
  assignment's instruction to use each group's "respective standard deviation
  together with the range."
- **Plot area:** deduced from the maximum trees observed per row (7) implying a
  nominal 7×7 planting grid at 3×3 m spacing = 441 m² per plot
- Full rationale and assumptions are documented in [`report/short_report.md`](report/short_report.md)

## Repository structure

| Folder | Contents |
|---|---|
| `data/` | Raw input spreadsheet (`inventario.xlsx`) |
| `notebooks/` | Jupyter notebook with the full commented analysis |
| `outputs/` | Generated tables (CSV/XLSX) and figures (PNG) for each question |
| `report/` | Short report with figures and interpretation |
| `docs/` | Original assignment PDF |

## How to reproduce

```bash
pip install pandas numpy matplotlib openpyxl
jupyter notebook notebooks/Quality_audit_Diameter.ipynb
```

The notebook auto-detects the `.xlsx` file inside `data/` — no path editing needed.

## Results overview

| Metric | Value |
|---|---|
| Trees measured | 215 |
| Plots sampled | 6 |
| Mean DBH (stand) | 15.82 cm |
| Basal area (stand average) | 16.52 m²/ha |
| Suspicious DBH values flagged (IQR) | 4 |
| Estimated trees ≥ 15 cm DBH (48.7 ha field) | ≈ 25,950 |

See [`report/short_report.md`](report/short_report.md) for full tables, figures, and
discussion.

## Author

Danial Hussain
Forest Management — [Professor Cristian] — 2nd Semester 2026
