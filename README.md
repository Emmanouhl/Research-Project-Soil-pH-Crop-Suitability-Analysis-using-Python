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

## Sample Output

<img width="1192" height="657" alt="RS" src="https://github.com/user-attachments/assets/16a9bf20-bd66-4501-9f46-1604d5ad99e3" />
<img width="1140" height="566" alt="RS1" src="https://github.com/user-attachments/assets/a4817cae-ba96-4d5f-b178-2bb8613f08d3" />
<img width="1114" height="572" alt="RS2" src="https://github.com/user-attachments/assets/c88651b6-bdea-4a2b-88d6-e374ee680a13" />
<img width="1093" height="558" alt="RS3" src="https://github.com/user-attachments/assets/4849f464-7a1e-4f26-9a35-49e4429c0082" />
<img width="1126" height="578" alt="RS4" src="https://github.com/user-attachments/assets/501ccace-7e64-4a59-8403-fa4a27a73b20" />
<img width="1110" height="562" alt="RS5" src="https://github.com/user-attachments/assets/c2a99a33-ea8b-4fd1-bac2-cf5eba0253e0" />
<img width="1116" height="563" alt="RS6" src="https://github.com/user-attachments/assets/32a10e78-6aca-473b-817b-c8518bbe411c" />
<img width="1111" height="556" alt="RS7" src="https://github.com/user-attachments/assets/0b62fee8-7426-48cb-afb9-d1637adf0029" />
<img width="1121" height="558" alt="RS8" src="https://github.com/user-attachments/assets/884d1cb0-75ce-473b-9bf3-e4434eea1516" />
<img width="1098" height="565" alt="RS9" src="https://github.com/user-attachments/assets/5e45cc6e-3182-45f2-9119-e1f2d1a79ad4" />
<img width="1104" height="557" alt="RS10" src="https://github.com/user-attachments/assets/642c0a4d-cf98-46aa-8f83-c2ceadbc4887" />
<img width="1094" height="563" alt="RS11" src="https://github.com/user-attachments/assets/14282404-7bf4-4478-8f3f-7395772e7660" />
<img width="1105" height="560" alt="RS12" src="https://github.com/user-attachments/assets/6631166c-9fbb-4950-985a-c9c4c508ce51" />
<img width="1107" height="561" alt="RS13" src="https://github.com/user-attachments/assets/1c16c7f5-c1f4-426c-89a1-73223c7fe8e3" />
<img width="1102" height="559" alt="RS14" src="https://github.com/user-attachments/assets/852fdcff-bbba-4d9b-a1d7-05f26df912c7" />
<img width="1115" height="553" alt="RS15" src="https://github.com/user-attachments/assets/2c253c15-248b-4cb0-a480-7a06efd391fa" />
<img width="1095" height="565" alt="RS16" src="https://github.com/user-attachments/assets/dae041a1-b1b2-40a7-82ad-8a740bb880bc" />
<img width="1105" height="562" alt="RS17" src="https://github.com/user-attachments/assets/99a268d0-8d0d-44e0-97be-f2d459c9dc95" />

---

## Project Structure

soil-ph-crop-suitability/

│

├── README.md

├── Research Project (Soil pH Crop Suitability Analysis).ipynb

│

├── data_raw/

│   ├── Nigeria_soil_data_preliminary.csv

│   └── README.md

│

├── figures/

│   ├── step5_spatial_basic.png

│   ├── step5_spatial_ph_coloured.png

│   ├── step6_ph_histogram.png

│   ├── step6_ph_boxplot.png

│   ├── step6_ph_by_depth.png

│   ├── step6_ph_classes.png

│   ├── step6_crop_suitability.png

│   ├── soil_ph_summary.csv

│   ├── step6_crop_suitability.csv

│   ├── step6_regional_ph.csv

│   └── step7_final_summary.csv

│

└── requirements.txt
