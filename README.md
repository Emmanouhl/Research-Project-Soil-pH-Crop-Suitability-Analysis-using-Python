# Soil pH Crop Suitability Analysis

A Python-based research project analysing soil pH distribution across Nigeria and its suitability for six common crops, using the **AfSIS Nigeria soil dataset** (accessed via iSDA).

---

## Table of Contents

- [Project Overview](#project-overview)
- [Research Aim](#research-aim)
- [Dataset](#dataset)
- [Methodology](#methodology)
- [Analyses Performed](#analyses-performed)
- [Key Findings](#key-findings)
- [Crop Suitability Results](#crop-suitability-results)
- [Recommendations](#recommendations)
- [Limitations](#limitations)
- [Technologies Used](#technologies-used)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Outputs](#outputs)
- [Authors](#authors)
- [License](#license)

---

## Project Overview

This project carries out a **descriptive analysis of soil pH in Nigeria** using Python. It combines statistics, spatial visualisation, and agronomic classification to answer practical questions about soil condition and crop suitability.

**Scope:** Soil pH only — the most widely used single indicator of soil condition, governing nutrient availability, microbial activity, and crop suitability.

---

## Research Aim

To describe the distribution and variability of soil pH across Nigeria, classify it into agronomic categories, and assess the suitability of sampled locations for six common Nigerian crops.

---

## Dataset

**Source:** AfSIS Nigeria soil dataset (accessed via iSDA)

| Attribute | Detail |
|-----------|--------|
| Records | 4,157 observations |
| Columns | 24 |
| Geographic coverage | Nigeria (sampled: 4.43°–11.72°E, 5.23°–11.62°N) |
| Source types | `afsis_spectral` (2,048) and `afsis_wetchem` (2,109) |
| Depth categories | Topsoil 0–20 cm (3,146) and subsoil 20–50 cm (1,011) |
| Variable of interest | `ph` (complete — no missing values) |

**Note on data handling:** The raw data file is never edited. All cleaning and filtering operates on in-memory copies.

---

## Methodology

The analysis follows a seven-step workflow:

| Step | Description |
|------|-------------|
| **Step 1** | Data Importation — load dataset, examine structure |
| **Step 2** | Geographic Filtering — retain records within Nigeria's boundaries |
| **Step 3** | Data Cleaning — check missing values, types, duplicates |
| **Step 4** | Descriptive Statistics — summarise pH using Pandas and NumPy |
| **Step 5** | Spatial Visualisation — scatter plot of longitude vs latitude, coloured by pH |
| **Step 6** | Distribution & Outlier Analysis — histogram, box plot, depth comparison, classification |
| **Step 7** | Interpretation & Reporting — patterns, relevance, limitations, conclusion |

---

## Analyses Performed

### Descriptive Statistics
- Mean, median, min, max, standard deviation
- Quartiles (Q1, Q3) and interquartile range (IQR)
- Skewness

### Spatial Analysis
- Basic scatter plot of sampling locations
- pH-coloured scatter plot (blue = acidic, red = alkaline)
- Cluster identification (rounded coordinates to 1-degree cells)

### Distribution Analysis
- Histogram (20 bins)
- Box plot with outlier identification (1.5 × IQR rule)
- Depth comparison (topsoil vs subsoil)

### Classification
- Agronomic pH classes:
  - Strongly acidic (< 4.5)
  - Acidic (4.5–5.5)
  - Slightly acidic (5.5–6.5)
  - Near neutral (6.5–7.5)
  - Alkaline (> 7.5)

### Crop Suitability
Assessed against published pH ranges for six crops:

| Crop | Suitable pH range |
|------|-------------------|
| Maize | 5.5 – 7.0 |
| Rice | 5.5 – 6.5 |
| Cassava | 5.5 – 6.5 |
| Groundnut | 6.0 – 7.0 |
| Cowpea | 6.0 – 7.0 |
| Tomato | 6.0 – 6.8 |

---

## Key Findings

### Distribution
- **Mean pH:** 5.918 | **Median:** 5.963
- **Range:** 3.990 – 7.945
- **Standard deviation:** 0.480 (low-to-moderate variability)
- **Skewness:** -0.336 (slightly skewed toward low pH)

### Outliers
- **73 outliers** (≈1.8% of observations) identified via 1.5 × IQR rule
- Most on the acidic side
- **Retained** in analysis per methodology

### Depth Comparison
- Topsoil mean: **5.958**
- Subsoil mean: **5.792**
- Difference: **0.166 pH units** (small — depth not a strong driver)

### pH Classification

| Class | Count | Percentage |
|-------|-------|------------|
| Slightly acidic | 3,019 | 72.6% |
| Acidic | 744 | 17.9% |
| Near neutral | 383 | 9.2% |
| Strongly acidic | 9 | 0.2% |
| Alkaline | 2 | <0.1% |

**≈91% of sampled locations fall below pH 6.5.**

### Regional Variation
- Cluster means ranged from **5.30** (10°E, 5°N) to **6.32** (10°E, 9°N)
- Most acidic clusters in the south
- No simple north–south or east–west gradient

---

## Crop Suitability Results

| Crop | Suitable pH range | Suitable locations | Percent suitable |
|------|-------------------|--------------------|------------------|
| **Maize** | 5.5 – 7.0 | 3,372 | **81.1%** |
| **Rice** | 5.5 – 6.5 | 3,019 | **72.6%** |
| **Cassava** | 5.5 – 6.5 | 3,019 | **72.6%** |
| Groundnut | 6.0 – 7.0 | 1,896 | 45.6% |
| Cowpea | 6.0 – 7.0 | 1,896 | 45.6% |
| **Tomato** | 6.0 – 6.8 | 1,831 | **44.0%** |

**Interpretation:** Maize, rice, and cassava are broadly compatible with the sampled soils. Groundnut, cowpea, and tomato would require **liming or careful site selection** at many locations.

---

## Recommendations

1. **For acidic soils (pH < 5.5):** Apply agricultural lime before planting pH-sensitive crops (maize, groundnut, tomato).
2. **For slightly acidic soils (pH 5.5–6.5):** Cassava, rice, and maize can be cultivated without liming.
3. **For near-neutral soils (pH 6.5–7.5):** Groundnut, tomato, and cowpea can generally be grown.
4. **Use local soil testing** — regional variation means national averages are misleading.
5. **Test before amending** — findings describe sampled patterns, not every farm.

---

## Limitations

- **pH alone is insufficient** — no nutrient, organic matter, texture, or salinity data analysed.
- **Uneven spatial sampling** — clusters at specific locations, not a national grid.
- **Two source types** — `afsis_spectral` and `afsis_wetchem` combined; method differences possible.
- **No crop or yield data** — cannot link pH to productivity.
- **Descriptive scope** — no spatial modelling or causal testing.

---

## Technologies Used

| Technology | Purpose |
|------------|---------|
| **Python 3.13** | Programming language |
| **Pandas** | Data manipulation and analysis |
| **NumPy** | Numerical operations |
| **Matplotlib** | Data visualisation |
| **Jupyter Notebook** | Interactive development environment |

---

## Project Structure
