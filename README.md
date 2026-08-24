# 🚧 Highway Footprint on Landscape Transformation

### Multi-Temporal Remote Sensing and GIS Assessment of Land-Cover Dynamics

[![Google Earth Engine](https://img.shields.io/badge/Google%20Earth%20Engine-4285F4?style=for-the-badge\&logo=googleearthengine\&logoColor=white)](https://earthengine.google.com/)
[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge\&logo=python\&logoColor=white)](https://www.python.org/)
[![Sentinel-2](https://img.shields.io/badge/Sentinel--2-ESA-003399?style=for-the-badge)](https://sentinel.esa.int/)
[![Dynamic World](https://img.shields.io/badge/Dynamic%20World-Google-4285F4?style=for-the-badge)](https://dynamicworld.app/)

---

## 📌 Overview

Rapid transportation infrastructure development is an important driver of landscape transformation. While highway development improves regional connectivity, accessibility, trade, and socioeconomic opportunities, associated land-use changes can place increasing pressure on forests, agricultural land, vegetation, wetlands, and other environmentally sensitive landscapes.

This project investigates the **spatial and temporal footprint of highway-associated landscape transformation** using multi-temporal satellite observations, Land Use/Land Cover (LULC) analysis, vegetation and built-up indices, transition analysis, fragmentation assessment, and development-pressure mapping.

The workflow combines **Google Earth Engine and Python-based geospatial analysis** to quantify how the landscape has changed over time and identify areas experiencing concentrated development pressure.

---

## 🎯 Objectives

The study is designed to:

* Analyze multi-temporal **Land Use/Land Cover (LULC)** dynamics.
* Quantify changes in major land-cover classes.
* Assess **built-up expansion** associated with development.
* Estimate **cropland loss** and agricultural-land transformation.
* Evaluate **vegetation and tree-cover loss**.
* Identify dominant **LULC transition pathways**.
* Analyze changes in **NDVI** as an indicator of vegetation condition.
* Analyze changes in **NDBI** as an indicator of built-up intensity.
* Assess **vegetation fragmentation and patch structure**.
* Identify spatial **development-pressure hotspots**.
* Integrate multiple indicators to understand the broader landscape response to infrastructure development.

---

## 🗺️ Study Framework

The analysis focuses on a predefined **5-km highway corridor**.

> **Important:** The study boundary is already represented by the uploaded 5-km corridor asset. No additional buffer is generated within the analysis.

The primary comparative period is:

**2016–2025**

A separate **2026 year-to-date** assessment is also included to provide an indication of the most recent landscape condition.

Because 2026 represents an incomplete year, it should **not be directly interpreted as equivalent to the complete-year observations from 2016–2025**.

---

## 🛰️ Data Sources

| Dataset                        | Purpose                 | Period    |
| ------------------------------ | ----------------------- | --------- |
| Google Dynamic World           | LULC classification     | 2016–2026 |
| Sentinel-2 Surface Reflectance | Spectral indices        | 2016–2026 |
| Highway corridor boundary      | Spatial analysis extent | —         |
| Derived LULC transitions       | Change detection        | 2016–2025 |
| Derived NDVI                   | Vegetation condition    | 2016–2025 |
| Derived NDBI                   | Built-up intensity      | 2016–2025 |

### Dynamic World Classes

| Class | Land Cover         |
| ----: | ------------------ |
|     0 | Water              |
|     1 | Trees              |
|     2 | Grass              |
|     3 | Flooded Vegetation |
|     4 | Crops              |
|     5 | Shrub & Scrub      |
|     6 | Built              |
|     7 | Bare               |
|     8 | Snow & Ice         |

---

# 🔬 Methodology

## 1. Multi-Temporal LULC Mapping

Annual Dynamic World observations are used to generate representative LULC maps using the **annual modal class**.

The analysis evaluates:

* 2016
* 2018
* 2020
* 2022
* 2024
* 2025
* 2026 YTD

For each year, the area occupied by individual land-cover classes is calculated in hectares.

---

## 2. LULC Change Detection

Land-cover transformation between **2016 and 2025** is assessed using pixel-level comparison.

The analysis identifies:

* unchanged areas
* changed areas
* class-specific gains
* class-specific losses
* spatial concentration of landscape transformation

The total area undergoing LULC change is also quantified.

---

## 3. LULC Transition Analysis

A transition matrix framework is used to identify major land-cover conversion pathways.

Transition coding follows:

```text
Old Class × 10 + New Class
```

For example:

```text
16 → Trees → Built
46 → Crops → Built
14 → Trees → Crops
47 → Crops → Bare
26 → Grass → Built
56 → Shrub → Built
```

This allows the spatial distribution and area of important transformation pathways to be mapped and quantified.

---

## 4. Built-Up Expansion

Built-up development is assessed by comparing the built-up class between 2016 and 2025.

The analysis identifies:

```text
Built-up 2016
        ↓
Built-up 2025
        ↓
New Built-up Areas
```

The resulting map represents areas that were not classified as built-up in 2016 but were classified as built-up in 2025.

---

## 5. Cropland Loss

Cropland dynamics are assessed by comparing:

* Cropland extent in 2016
* Cropland extent in 2025
* Areas converted from cropland to other land-cover classes

Particular attention is given to **cropland-to-built-up conversion** as an indicator of development-driven agricultural-land transformation.

---

## 6. Vegetation and Tree-Cover Loss

Vegetation is defined using the following Dynamic World classes:

* Trees
* Grass
* Flooded Vegetation
* Crops
* Shrub & Scrub

Vegetation loss is identified where areas classified as vegetation in 2016 no longer belong to a vegetation class in 2025.

A separate analysis is conducted for **tree-cover loss**.

---

# 🌿 Vegetation Condition Analysis

## NDVI

The Normalized Difference Vegetation Index (NDVI) is calculated using Sentinel-2:

[
NDVI = \frac{NIR - Red}{NIR + Red}
]

For Sentinel-2:

* NIR = B8
* Red = B4

NDVI is used to evaluate spatial and temporal variation in vegetation condition.

The study evaluates:

* NDVI 2016
* NDVI 2020
* NDVI 2025
* NDVI 2026 YTD
* NDVI change between 2016 and 2025

Areas showing substantial NDVI decline are identified as potential zones of vegetation degradation or landscape disturbance.

---

# 🏙️ Built-Up Intensity Analysis

## NDBI

The Normalized Difference Built-up Index (NDBI) is calculated as:

[
NDBI = \frac{SWIR - NIR}{SWIR + NIR}
]

For Sentinel-2:

* SWIR = B11
* NIR = B8

NDBI is used to characterize the spatial pattern of built-up intensity.

The analysis focuses on:

* NDBI 2016
* NDBI 2020
* NDBI 2025
* NDBI change between 2016 and 2025

An increase in NDBI, when interpreted alongside LULC and NDVI information, can indicate areas undergoing increasing built-up or surface-development pressure.

---

# 🌳 Landscape Fragmentation

Vegetation fragmentation is assessed using spatial patch analysis.

The workflow evaluates:

* vegetation patch size
* small vegetation patches
* core vegetation
* spatial distribution of fragmented vegetation

Connected-pixel analysis is used to identify the structural characteristics of vegetation patches.

A focal morphological operation is additionally applied to identify areas representing **core vegetation**.

---

# 🔥 Development Pressure Mapping

A composite **Development Pressure Index** is generated using multiple indicators:

### Components

1. New built-up development
2. Cropland → Built-up conversion
3. Trees → Built-up conversion
4. NDVI decline
5. NDBI increase

The development-pressure score is calculated by combining these indicators using weighted contributions.

Higher scores indicate locations where multiple indicators of landscape transformation occur simultaneously.

---

## Development Hotspots

Areas with a development-pressure score of **≥ 4** are classified as high-development hotspots.

These locations represent areas where:

* built-up expansion is occurring,
* productive land is being converted,
* vegetation is declining,
* and/or built-up intensity is increasing.

The hotspot layer provides a spatial basis for identifying areas requiring closer environmental monitoring and planning attention.

---

# 📊 Key Analytical Outputs

The workflow generates the following major outputs:

### LULC

* Annual LULC maps
* LULC area statistics
* LULC change map
* LULC transition map

### Development

* Built-up expansion map
* New built-up area statistics
* Development-pressure map
* High-development hotspot map

### Agriculture

* Cropland distribution
* Cropland loss map
* Cropland-to-built-up transition

### Vegetation

* Vegetation-loss map
* Tree-cover loss map
* NDVI maps
* NDVI-change map
* Vegetation patch-size map
* Small vegetation patches
* Core vegetation map

### Built-Up Environment

* NDBI maps
* NDBI-change map

---

# 📁 Repository Structure

```text
.
├── README.md
│
├── gee/
│   └── highway_landscape_transformation.js
│
├── python/
│   ├── lulc_visualization.py
│   ├── raster_analysis.py
│   └── change_analysis.py
│
├── data/
│   └── study_boundary/
│
├── outputs/
│   ├── lulc/
│   ├── transitions/
│   ├── vegetation/
│   ├── builtup/
│   ├── indices/
│   └── hotspots/
│
└── figures/
    ├── lulc_maps/
    ├── change_maps/
    ├── ndvi/
    ├── ndbi/
    └── development_hotspots/
```

---

# 🧰 Technologies Used

* **Google Earth Engine**
* **Python**
* **Rasterio**
* **NumPy**
* **Matplotlib**
* **GeoPandas**
* **Sentinel-2**
* **Google Dynamic World**
* **Remote Sensing**
* **GIS**
* **Land Use/Land Cover Change Detection**

---

# 📈 Analytical Workflow

```text
Highway Corridor
       │
       ▼
Multi-Temporal Satellite Data
       │
       ├───────────────┐
       ▼               ▼
Dynamic World      Sentinel-2
       │               │
       ▼               ▼
     LULC         NDVI / NDBI
       │               │
       ▼               ▼
LULC Change      Index Change
       │               │
       ├───────┬───────┘
       ▼       ▼
Transitions  Vegetation
       │      Fragmentation
       │       │
       └───┬───┘
           ▼
   Development Pressure
           │
           ▼
    Hotspot Identification
           │
           ▼
 Landscape Transformation
           │
           ▼
Sustainable Land-Use
and Infrastructure Planning
```

---

# ⚠️ Important Analytical Considerations

* The study boundary represents an **existing 5-km corridor**; no additional buffer is generated.
* The principal change-detection period is **2016–2025**.
* **2026 is year-to-date** and should be interpreted separately from complete-year observations.
* NDVI and NDBI are interpreted together with LULC information rather than as standalone indicators of land-cover conversion.
* Development-pressure mapping is a **relative composite indicator**, not a direct measurement of infrastructure impact.
* LULC transitions represent observed land-cover changes within the study corridor and should not automatically be interpreted as causally attributable to the highway without additional causal or distance-based analysis.
* A formal **distance-gradient analysis** requires a road centreline and explicit distance-based zones; the current workflow does not independently calculate such gradients.

---

# 🌍 Significance

Understanding the environmental footprint of transportation infrastructure is essential for balancing connectivity and economic development with ecological sustainability.

This framework provides a spatially explicit approach for identifying:

* where development is concentrated,
* which land-cover classes are most affected,
* how agricultural and vegetated landscapes are transformed,
* where vegetation condition is declining,
* how fragmentation is emerging,
* and where multiple development indicators converge.

The resulting information can support **evidence-based infrastructure planning, environmental monitoring, landscape management, and sustainable regional development**.

---

# 🚀 Future Improvements

Potential extensions of this project include:

* Road-centreline-based distance-gradient analysis
* Multi-ring buffer analysis
* Landscape metrics such as FRAGSTATS-style indices
* Shannon's Diversity Index
* Patch Density
* Edge Density
* Landscape Shape Index
* Mean Patch Size
* Connectivity analysis
* Land Surface Temperature analysis
* Rainfall and climate-variable integration
* Hydrological and wetland-impact assessment
* Statistical testing of LULC trends
* Machine-learning-based development-pressure modelling
* Validation using high-resolution imagery and field observations

---

# 📚 Citation

If you use this workflow, datasets, maps, or derived outputs in research, please cite the relevant datasets and acknowledge the analytical workflow used in this repository.

---

## 👨‍💻 Author

**Jintu Bhuyan**

Remote Sensing & GIS | Geospatial Analysis | Environmental Monitoring | Earth Observation

---

## ⭐ Project Focus

> **From infrastructure expansion to landscape transformation — using Earth observation to understand how development reshapes the environment.**
