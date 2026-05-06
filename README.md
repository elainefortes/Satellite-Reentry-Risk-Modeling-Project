# Orbital Analysis of Active Satellites

This repository contains a complete pipeline for processing, classifying, and visualizing orbital data using the `active_satellites.csv` dataset. The code was developed to organize exploratory analyses, generate risk metrics, identify anomalies, group orbital regimes, and produce visualizations intended for technical reports and scientific articles.

The project is organized into independent modules, which can be executed separately or as an integrated workflow.

---

## General Pipeline Structure

### Module 1 — Environment Setup
- Google Drive mounting (for Google Colab usage).
- Import of the main libraries.
- Visualization settings.
- CSV loading and verification of essential columns.
- Altitude calculation when necessary.

---

### Module 2 — Descriptive Analyses
Includes:
- Classification by country, mission type, and constellation.
- Distribution by altitude, inclination, eccentricity, drag term (BSTAR), and orbital regime.
- Generation of plots and tables in PNG format.

---

### Module 3 — Global Map by Latitudinal Regions
- Use of Cartopy for global visualization.
- Satellite distribution according to latitude bands derived from orbital inclination.
- Color-based representation with simulated point distributions.

---

### Module 4 — Geosynchronous Satellite (GEO) Classification
Application of standard GEO criteria:
- Mean Motion close to 1 rev/day,
- Inclination below 5 degrees,
- Low eccentricity,
- Altitude near 35,786 km.

This module generates comparative plots and exports the classified satellites.

---

### Module 5 — Orbital Clustering with K-Means
- Number of clusters defined as \(k = 4\).
- Variables used: inclination, mean motion, eccentricity, and RAAN.
- Identification of the dominant orbital regime within each cluster.
- Generation of percentages and LaTeX-ready output lines.

---

### Module 6 — Heuristic Reentry Risk Classification
Classification based on:
- perigee altitude,
- eccentricity,
- BSTAR,
- REV_AT_EPOCH.

Includes:
- histograms of risk categories,
- eccentricity versus altitude plots in logarithmic scale,
- export of consolidated tables.

---

### Module 7 — Anomaly Identification with Isolation Forest
- Standardization of input variables.
- Automatic contamination rate adjustment.
- Support for different atmospheric scenarios (global warming, geomagnetic storms, and future projections).
- Generation of score distribution plots and scatter diagrams.
- Export of detected anomalies to CSV files.

---

### Module 8 — Unified Risk Classification Pipeline (Random Forest)
- Construction of noisy risk labels with controlled perturbations.
- Training with cross-validation.
- Metrics reported: accuracy, weighted F1-score, confusion matrix, and feature importance.
- Comparison among three scenarios: current conditions, global warming, and geomagnetic storm conditions.

---

### Module 9 — Graphical Comparisons Between Scenarios
This module produces:
- comparative scatter plots,
- histograms by risk category,
- cumulative altitude distribution curves (CDF),
- summary tables.

---

### Module 10 — Global Heatmap
- Conversion of risk categories into numerical weights.
- Simulation of longitudinal positions.
- Generation of an interactive HTML map using Folium.

---

## Cells A, B, and C — Altitude Loss Simulation During Storm Conditions

These cells extend the pipeline with a simplified physical model to estimate altitude decay caused by increased atmospheric density during geomagnetic storms.

### Cell A — Parameterization and Auxiliary Functions
Responsible for:
- selecting satellites in LEO (between 120 and 1200 km),
- verifying the required columns,
- defining the simulation interval (72 hours with 1-hour steps),
- generating a synthetic Kp index profile,
- defining atmospheric density and decay factor functions.

All preparation for numerical integration is carried out in this stage.

---

### Cell B — Numerical Integration of Altitude (Storm Scenario)
Performs the full altitude decay simulation:
- explicit integration over 72 hours,
- use of the Kp profile to increase atmospheric drag,
- calculation of final altitude and total altitude loss per satellite.

Outputs include:
- decay statistics,
- average time series by altitude band,
- histograms,
- list of the most affected satellites.

---

### Cell C — Comparison Between Storm and Quiet Conditions
Performs a second integration assuming constant low Kp values:
- direct comparison between storm and quiet scenarios,
- calculation of differences between final altitudes,
- generation of comparative plots by altitude band,
- export of consolidated tables.

---

## Main Dependencies

- Python 3.x  
- NumPy  
- Pandas  
- Matplotlib  
- Seaborn  
- Cartopy  
- scikit-learn  
- Folium  

This project was developed using Google Colab.
