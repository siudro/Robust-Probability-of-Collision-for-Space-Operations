# DebriSolver Competition: Space Debris Conjunction Analysis

Comprehensicve analysis of Conjunction Data Messages (CDMs) and  collision risks assessment  in Low Earth Orbit (LEO)

## Overview

This repository contains two complementary notebooks for space debris risk analysis:

1. **Exploratory Data Analysis (EDA)** - Deep dive into CDM datasets
2. **Hybrid Collision Probability Filter** - Advanced Monte Carlo validation system

## Notebooks

### 1. `CDM_AI_BrainStorm.ipynb` - Exploratory Analysis
**Purpose:** Comprehensive exploration of space traffic patterns and operational risks

**Key Features:**
- Traffic pattern analysis (Payload-Payload vs Payload-Debris encounters)
- Temporal risk assessment (warning time distributions)
- Geographic threat mapping (orbital altitude clustering)
- Historical debris source identification (Fengyun 1C, COSMOS 2251, etc.)
- Operational dashboard for real-time risk monitoring

**Key Findings:**
- 71.5% of conjunctions are intra-constellation (Payload vs Payload)
- 55% of high-risk, late-warning events caused by active satellites (coordination failures)
- Fengyun 1C debris cloud remains the #1 external threat

### 2. `debrisolver_hybrid_pc_main.ipynb` - Monte Carlo Validation
**Purpose:** Validate analytic collision probabilities using Monte Carlo simulation

**Key Features:**
- Encounter-plane geometry transformation (RTN to collision frame)
- Validity gating (size-ratio, tangency, curvature metrics)
- Parallel Monte Carlo simulation for high-risk events
- False-positive reduction through physics-based filtering

**Results:**
- Identifies "nightmare scenarios" (high Pc + late warning)
- Quantifies false-positive rates in analytic probability calculations
- Provides MC-confirmed risk assessments for operational decisions

### Monte Carlo Validation
```python
# Apply validity gates
eta, T, rho = gating_metrics(row)
needs_mc = (eta > 0.6) | (T > 0.95) | (rho > 0.2)

# Run MC simulation
mc_result = mc_pc_encounter_plane(row, nsamp=100_000)
```

## Key Thresholds

| Metric | Threshold | Meaning |
|--------|-----------|---------|
| **Collision Probability** | > 1×10⁻⁴ | Physics "Red Zone" |
| **Warning Time** | < 24 hours | Operational emergency |
| **Size Ratio (η)** | > 0.6 | Analytic method may fail |
| **Tangency (T)** | > 0.95 | Nearly tangent encounter |
| **Curvature (ρ)** | > 0.2 | Orbital curvature significant |

## Applications

- **Satellite operators:** Collision avoidance maneuver planning
- **Space traffic management:** Coordination failure identification
- **Debris mitigation:** Historical threat source analysis
- **Research:** Mega-constellation risk modeling

## Key Insights

### The Three-Front War
1. **Uncooperative Neighbors** (Active satellites with poor coordination)
2. **Stealth Assassins** (Small debris at sensor detection limits)
3. **Weather Vanes** (High area-to-mass ratio objects affected by solar activity)

### Operational Reality
- Most "emergency" alerts come from active satellites, not debris
- Fengyun 1C (2007 ASAT test) remains dominant debris threat after 18 years
- Modern rocket bodies (CZ-6A) represent emerging pollution source

