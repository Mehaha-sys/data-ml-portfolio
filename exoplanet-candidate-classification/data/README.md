# Dataset Documentation

"kepler_koi_dr25.csv"

This directory contains the dataset used in the Exoplanet Candidate Classification project.

The CSV is based on NASA's Kepler Objects of Interest (KOI) catalogue, which records astronomical observations and measurements associated with potential exoplanet detections.

## Purpose

The dataset is used to investigate whether confirmed exoplanets can be distinguished from false-positive detections using a reduced set of measured features.

## Dataset Overview

- File: "kepler_koi_dr25.csv"
- Format: CSV (Comma-Separated Values)
- Original dataset size: 8,054 rows and 141 columns
- Source: "NASA Exoplanet Archive — KOI Table Documentation" (https://exoplanetarchive.ipac.caltech.edu/docs/API_kepcandidate_columns.html)

The dataset includes transit measurements, signal characteristics, and stellar and planetary properties.

## Data Processing

The analysis notebook:

1. Loads the original dataset into a working DataFrame.
2. Retains confirmed objects and false positives for binary classification.
3. Excludes objects labelled as candidates.
4. Selects 26 candidate measurements and removes three unusable features.
5. Uses the remaining 23 features for baseline model training and evaluation.

The original CSV is preserved, while filtering, preprocessing, and missing-value imputation are performed during analysis.

## Important Notes

- The dataset contains astronomical measurements and catalogue classifications; not every object represents a confirmed planet.
- Missing values are handled during model preprocessing.
- The catalogue's disposition labels are used to define the target variable and should not be used as predictive features.
- Refer to ""Exoplanet_Candidate_Classification.ipynb"" (../Exoplanet_Candidate_Classification.ipynb) for the full workflow.

## Data Source and Attribution

The dataset is based on the Kepler Objects of Interest catalogue. Please consult NASA's documentation for official field definitions, units, and applicable data-use guidance.

---

#### Related project: "Exoplanet Candidate Classification" (../README.md)
