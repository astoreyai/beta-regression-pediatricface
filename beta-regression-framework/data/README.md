# Data Sources

This directory contains documentation for data used in the beta regression analysis.

## Synthetic Data Only

This paper uses only synthetic data generated computationally. No real biometric samples from children were collected or used.

### Ethics Statement
As stated in the paper (Section: Ethics Statement):
> "This research uses only synthetic data generated computationally to match published degradation patterns from the literature. No human subjects were involved in data collection for this study. The synthetic datasets were calibrated to aggregate statistical patterns reported in peer-reviewed publications (Deb et al., Bahmani et al.) and do not contain any identifiable information or biometric samples from real individuals. Therefore, institutional review board approval was not required for this purely methodological work."

## Synthetic Data Generation

The simulations generate synthetic longitudinal data calibrated to published patterns from:

### Source 1: Young Face Aging (YFA) Dataset
- **Reference**: Bahmani et al. (2023), "Longitudinal Evaluation of Child Face Recognition and the Impact of Underlying Age"
- **Original Dataset**: 330 subjects, 3,831 images, 6-month intervals, 8-year period, ages 3-18
- **What we used**: Age-specific degradation patterns (Table 3 from paper)
  - Ages 3-5: 97.8% to 63.1% over 6.5-8 years
  - Ages 5.5-7: 97.9% to 80.2% (most stable)
  - Ages 7.5-9: 98.3% to 65.6% (intermediate)

### Source 2: Children Longitudinal Face (CLF) Dataset
- **Reference**: Deb et al. (2018), "Longitudinal Study of Child Face Recognition"
- **Original Dataset**: 919 subjects, 3,682 images, ages 2-18, up to 7-year tracking
- **What we used**: Statistical modeling approaches and degradation estimates (approximately 0.22 SD per year)

## Our Simulation Parameters

```python
# Simulation formula (Section 6.1)
TAR_ij ~ Beta(μ_ij · φ, (1-μ_ij) · φ)

# Parameters calibrated to YFA patterns:
u_i ~ N(0, σ_u²)  where σ_u = 0.03  # between-subject variation
φ = 50                               # precision parameter

# Age-specific slopes:
β₂ = -0.35  # Ages 3-5 (steep decline)
β₂ = -0.08  # Ages 5.5-7 (stability)
β₂ = -0.20  # Ages 7.5-9 (delayed degradation)

# Sample size:
100 subjects per age group (300 total)
Annual observations over 8 years
```

## Code Location

Simulation code is available in:
- `supplementary/notebooks/StoreyAaron_BetaRegression.ipynb` (Statistical models)
- `supplementary/notebooks/StoreyAaron_ChildFaceAnalysis.ipynb` (Data exploration)

## Validation on Real Data

### Validation Protocol (Section 8.5)
The paper provides a detailed protocol for researchers with access to real datasets:

**Phase 1: Direct Replication**
- Fit beta regression to actual TAR trajectories
- Compare boundary violations between linear and beta models
- Hypothesis: 0% violations (beta) versus 5-10% (linear)

**Phase 2: Predictive Validation**
- Temporal split: train on years 0-4, test on years 5-8
- Evaluate out-of-sample accuracy and confidence interval calibration
- Hypothesis: 95% +/- 2% CI coverage

**Phase 3: Operational Validation**
- Calculate re-enrollment intervals for 80% TAR threshold
- Validate age-specific recommendations
- Test demographic robustness

### Accessing Real Datasets

For researchers seeking to validate on real data:

| Dataset | Contact | Details |
|---------|---------|---------|
| **Children Longitudinal Face (CLF)** | Deb et al. (2018) authors | 919 children, ages 2-18, 2-7 year tracking |
| **Young Face Aging (YFA)** | Bahmani et al. (2023) authors | 330 subjects, ages 3-18, 8-year tracking, 6-month intervals |

## Repository Structure

This directory is intentionally empty because:
1. The paper uses synthetic data only (no real biometric samples)
2. Real datasets require permission from original authors
3. Simulation code generates data during analysis (not pre-stored)

## Note on Data Availability Statement

From the paper (Section: Data Availability):
> "The simulation code, synthetic datasets, and analysis scripts used in this study are available at: https://github.com/astoreyai/beta-regression-pediatricface. The repository provides Python implementations of the simulation code, synthetic datasets calibrated to match YFA patterns, and Jupyter notebooks for reproducing all analyses, including beta regression model fitting using Python's statsmodels library."

For questions about data generation or validation protocols, contact: storeyaw@clarkson.edu, mimtiaz@clarkson.edu, or smondal@clarkson.edu
