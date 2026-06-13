<div align="center">

# 🛰️ BhuMe Boundary Alignment Challenge

### Geospatial Boundary Correction using Satellite Imagery & Cadastral Maps

![Python](https://img.shields.io/badge/Python-3.12+-blue.svg)
![GeoPandas](https://img.shields.io/badge/GeoPandas-Geospatial-success)
![Shapely](https://img.shields.io/badge/Shapely-Geometry-orange)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

</div>

---

# 📌 Problem Statement

Historical cadastral maps often do not perfectly align with modern satellite imagery due to:

- Legacy surveying techniques
- Georeferencing errors
- Local distortions
- Digitization inaccuracies

The objective is to determine whether an official land parcel boundary can be **corrected** and generate an improved boundary representation while preserving consistency with the cadastral record.

---

# 🎯 Objective

For every plot in a village:

- Analyze the official cadastral geometry
- Estimate its displacement from the true field
- Produce a corrected boundary when confident
- Export predictions in the required `predictions.geojson` format

---

# 🏗️ Methodology

The implemented pipeline follows these steps:

```
Official Cadastral Map
            │
            ▼
Load Village Dataset
            │
            ▼
Read Example Ground Truths
            │
            ▼
Estimate Global Median Translation
            │
            ▼
Apply Translation to Official Plots
            │
            ▼
Generate predictions.geojson
            │
            ▼
Evaluate using Provided Scoring Tool
```

---

# ⚙️ Approach

## Step 1

Load:

- `input.geojson`
- `imagery.tif`
- `boundaries.tif`
- `example_truths.geojson`

---

## Step 2

Convert geometries into a projected coordinate system (UTM) for accurate distance calculations.

---

## Step 3

For each example truth:

```
dx = Truth Centroid X − Official Centroid X

dy = Truth Centroid Y − Official Centroid Y
```

---

## Step 4

Compute:

- Median ΔX
- Median ΔY

to estimate a village-level translation.

---

## Step 5

Apply the translation to every cadastral polygon:

```
Corrected Geometry

=

Official Geometry

+

(Median ΔX, Median ΔY)
```

---

## Step 6

Generate:

```
predictions.geojson
```

containing:

- plot_number
- status
- confidence
- method_note
- geometry

---

# 📊 Local Evaluation

## ✅ Vadnerbhairav

| Metric | Result |
|---------|---------|
| Median IoU | **0.713** |
| Official | 0.612 |
| Improvement | **+0.112** |
| Accurate (IoU ≥ 0.5) | **100%** |

---

## ✅ Malatavadi

| Metric | Result |
|---------|---------|
| Median IoU | **0.588** |
| Official | 0.510 |
| Improvement | **+0.090** |
| Accurate (IoU ≥ 0.5) | **67%** |

---

# 🧠 Design Philosophy

The goal of this implementation was to build a **simple, explainable, and reproducible baseline** rather than an over-engineered solution.

The emphasis was on:

- Robustness
- Generalization
- Interpretability
- Clean implementation

---

# 🚀 Potential Improvements

Given additional development time, the following enhancements could significantly improve performance:

- Image-based local alignment
- Boundary contour extraction
- Per-plot adaptive translation
- Confidence calibration
- Automatic uncertainty detection
- Hybrid classical vision + learning-based refinement

---

# 🛠️ Tech Stack

- Python
- GeoPandas
- Shapely
- Rasterio
- NumPy
- SciPy
- Pillow

---

# 📂 Repository Structure

```
.
├── bhume/
├── data/
│   ├── Vadnerbhairav/
│   │      predictions.geojson
│   └── Malatavadi/
│          predictions.geojson
├── transcripts/
├── quickstart.py
├── pyproject.toml
└── README.md
```

---

# 💡 Key Takeaways

This project demonstrates:

- Geospatial data processing
- Coordinate system transformations
- Geometry manipulation
- End-to-end prediction pipeline
- Evaluation against ground truth
- Practical engineering under uncertainty

---

<div align="center">

### Thank you for reviewing my submission.

**Anil Kumar**

</div>