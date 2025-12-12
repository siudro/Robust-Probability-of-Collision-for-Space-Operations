# DebriSolver Competition: Space Debris Conjunction Analysis

Comprehensive analysis of Conjunction Data Messages (CDMs) and collision risk assessment in Low Earth Orbit (LEO).

## Overview

This repository contains two complementary notebooks for space debris risk analysis developed for the DebriSolver competition:

1. **Exploratory Data Analysis (EDA)** – Content-driven exploration of CDM datasets  
2. **Hybrid Collision Probability Filter** – Physics-based analytic + Monte Carlo validation framework

## Dataset

This work uses the **Aldoria CDM dataset**, provided as part of the conjunction risk use case.

Dataset download link:  
https://drive.google.com/file/d/1tBwJmrstUN9LAC3eKOJ_UkD0SZw6g00w/view?usp=sharing

Download the dataset and place the CSV file in the repository root before running the notebooks.

## Notebooks

### 1. `Understanding_Aldoria_CDM_Dataset.ipynb` – Exploratory Analysis

**Purpose:** Comprehensive exploration of space traffic patterns and operational risks using CDM-only inputs.

**Key Features:**
- Traffic pattern analysis (Payload–Payload vs Payload–Debris encounters)
- Temporal risk assessment (warning time distributions)
- Orbital altitude clustering and traffic density
- Historical debris source identification (Fengyun 1C, COSMOS 2251, etc.)
- Content exploration aimed at operational understanding

**Key Findings:**
- ~71% of conjunctions are intra-constellation (Payload vs Payload)
- ~55% of high-risk, late-warning events are caused by active satellites
- Fengyun 1C debris remains the dominant external debris threat

---

### 2. `debrisolver_hybrid_pc_main.ipynb` – Hybrid Analytic–Monte Carlo Validation

**Purpose:** Validate catalog analytic collision probabilities using encounter-plane geometry and targeted Monte Carlo simulation.

**Key Features:**
- Encounter-plane geometry construction from CDM state and covariance
- Validity gating (size ratio, tangency, curvature metrics)
- Physics red-zone screening (Pc > 1×10⁻⁴)
- Parallel Monte Carlo simulation for selected events
- Quantification of analytic false positives

**Results:**
- Identifies “nightmare scenarios” (high risk with <24 h warning)
- Reduces false positives within the analytic red zone
- Produces MC-confirmed collision probabilities for operational decision support

## How to run

1. Download the Aldoria CDM dataset from the link above.
2. Place the CSV file in the repository root directory.
3. Open the notebooks using Jupyter Lab or Jupyter Notebook.
4. Run the notebooks top to bottom:
   - `Understanding_Aldoria_CDM_Dataset.ipynb` for exploratory analysis
   - `debrisolver_hybrid_pc_main.ipynb` for the hybrid analytic–Monte Carlo filter

The notebooks are self-contained and require only standard Python scientific libraries
(NumPy, Pandas, Matplotlib, Seaborn, Joblib).

---

### Monte Carlo Validation (core logic)

```python
# Apply validity gates
eta, T, rho = gating_metrics(row)
needs_mc = (eta > 0.6) | (T > 0.95) | (rho > 0.2)

# Run MC simulation
mc_result = mc_pc_encounter_plane(row, nsamp=100_000)
