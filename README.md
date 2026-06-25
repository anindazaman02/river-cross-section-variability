# Quantitative Morphodynamics and Statistical Variability Modeling of River Cross-Sections

[![Language](https://img.shields.io/badge/Language-R%20%2F%20RStudio-blue?logo=r&logoColor=white)](https://www.r-project.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 📌 Project Overview
This repository contains a specialized hydrological data-engineering pipeline written in R to quantify structural changes and elevation variability across river cross-sections. Ingesting multi-year field survey datasets (Distance and Reduced Level tracking) for **Station RMBR27**, the script integrates the channel cross-sectional boundary area while computing high-tier dispersion metrics (Standard Deviation and Standard Error). 

This pipeline serves as an empirical framework for monitoring channel bed stability, thalweg migration, and sediment scour-deposition patterns across dynamic river systems.

---

## 📊 Methodological Framework & Calculations

The R script executes an automated workflow optimized for river bathymetry processing:

### 1. Data Sanitization & Datetime Parsing
* Filters out incomplete observation records (`NA`) across distance and elevation parameters to secure numerical consistency.
* Extracts the calendar `Year` string out of multi-format field timestamps (`DATE`) using regularized date conversions within the `dplyr` mutations pipeline.

### 2. Volumetric Geometry Integration
* Computes the net cross-sectional profile area ($\text{m}^2$) by applying the **Trapezoidal Rule** via the `pracma::trapz()` integration function:
  $$\text{Area} = \int_{a}^{b} f(x) \,dx \approx \sum_{i=1}^{n-1} \frac{f(x_i) + f(x_{i+1})}{2} (x_{i+1} - x_i)$$
* Maps this mathematical integral dynamically across localized channel configurations across changing survey years.

### 3. Bed Elevation Variability & Dispersion Statistics
To provide deep insights into the unevenness, ruggedness, or shifting of the riverbed, data arrays are grouped by year to calculate:
* **Thalweg Baseline (Min RL):** Pinpoints the absolute deepest point of the river channel to log maximum vertical scouring.
* **Standard Deviation ($\text{SD}_{\text{RL}}$):** Measures the overall structural roughness and elevation dispersion across the channel layout.
* **Standard Error ($\text{SE}_{\text{RL}}$):** Estimates the precision of the sample mean relative to the true channel cross-section distribution:
  $$\text{SE} = \frac{\sigma}{\sqrt{n}}$$

### 4. Visual Cross-Section Profile Rendering
* Compiles a highly scannable multi-temporal line plot using the `ggplot2` visualization library. 
* Traverses the `Distance` coordinates on the X-axis against the vertical height changes (`RL` in meters) on the Y-axis, rendering separate color-coded profiles for each monitored year to provide quick visual proof of bank erosion or bed aggradation.

---

## 💻 Repository Structure & Usage

### File Directory
* `cross_section_variability_analysis.R` — Main statistical processing code for the R environment.

### Prerequisites & Dependencies
To deploy this project framework locally, ensure you have R/RStudio active along with the following libraries:
```r
install.packages(c("readxl", "dplyr", "ggplot2", "pracma"))
