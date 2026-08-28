# River Cross-Section Variability Analysis (Station RMBR27)

[![Language](https://img.shields.io/badge/Language-R-blue)](https://www.r-project.org/)

## Overview
This is an R script I developed to analyze river channel cross-sections and track elevation variability over time. Using historical field survey data for Station RMBR27, the code calculates the cross-sectional area and computes statistical metrics like Standard Deviation and Standard Error. It’s a practical way to monitor bed stability, channel roughness, and sediment scouring or deposition patterns.

## How the Script Works
The workflow processes the raw survey data to extract both physical dimensions and statistical variability:

* **Data Prep:** It reads the raw survey data, drops any missing coordinate rows to ensure the math works correctly, and pulls the survey year from the date column.
* **Area Calculation:** The script calculates the net cross-sectional area for each year using the Trapezoidal Rule via the `pracma::trapz()` function.
* **Variability Stats:** It groups the data by year to find the Thalweg (Minimum RL, which is the absolute deepest point of the channel). It also calculates the Standard Deviation (SD) to measure the overall roughness or unevenness of the riverbed, and the Standard Error (SE) for the sample mean.
* **Visualization:** It uses `ggplot2` to plot distance against elevation, generating a multi-year, color-coded line chart so you can easily see how the river profile has shifted or eroded over time.

## How to Run It
You will need R and RStudio installed, along with these packages:
```r
install.packages(c("readxl", "dplyr", "ggplot2", "pracma"))
