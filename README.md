# Beta Regression Framework for Child Face Recognition: A Methodological Framework with Simulation-Based Validation

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Paper Status](https://img.shields.io/badge/Status-Ready%20for%20Submission-brightgreen.svg)](https://github.com/astoreyai/Dissertation)

## Overview

This repository contains dissertation research addressing a critical methodological gap in child face recognition: when linear mixed models are inappropriately applied to bounded True Accept Rates (TAR), they can produce physically impossible predictions exceeding 100% accuracy. Our beta regression framework ensures mathematically valid predictions while providing superior variance modeling for operational biometric systems.

**Paper Status**: Manuscript complete and ready for IEEE T-BIOM submission (14 pages)

**Critical Finding**: In our simulation calibrated to published patterns, linear models produced 229 invalid predictions (>100% or <0%), while beta regression maintained 100% valid predictions with comparable fit (RMSE difference: 0.0016).

## Authors

**Aaron W. Storey** (Member, IEEE)
Ph.D. Candidate, Computer Science
Clarkson University, Potsdam, NY, USA
storeyaw@clarkson.edu | ORCID: [0009-0009-5560-0015](https://orcid.org/0009-0009-5560-0015)

**Masudul H. Imtiaz**
Assistant Professor, Electrical & Computer Engineering
Director, AI Vision, Health, Biometrics, and Applied Computing (AVHBAC) Lab
Clarkson University, Potsdam, NY, USA
mimtiaz@clarkson.edu | ORCID: [0000-0001-5528-482X](https://orcid.org/0000-0001-5528-482X)

## Repository Structure

```
Dissertation/
├── README.md                           # This file
├── beta-regression-framework/          # Beta Regression Research
│   ├── manuscript/                     # IEEE T-BIOM submission (14 pages)
│   │   ├── paper.pdf                  # Compiled manuscript (1.54 MB)
│   │   ├── paper.tex                  # LaTeX source
│   │   ├── references.bib             # 31 references
│   │   └── compile_paper.sh           # Compilation script
│   ├── figures/                        # All 6 publication figures
│   │   ├── age_patterns.pdf
│   │   ├── boundary_violations.pdf
│   │   ├── beta_regression_concepts.pdf
│   │   ├── variance_analysis.pdf
│   │   ├── prediction_intervals.pdf
│   │   └── operational_impact.pdf
│   ├── supplementary/
│   │   ├── notebooks/                 # Jupyter analysis
│   │   │   ├── StoreyAaron_BetaRegression.ipynb
│   │   │   └── StoreyAaron_ChildFaceAnalysis.ipynb
│   │   ├── presentations/
│   │   └── references/                # Bahmani 2023, Deb 2018 PDFs
│   ├── data/                          # See data/README.md
│   └── README.md                      # Detailed project description
└── [Future: Memory-Augmented Transformers]
```

## Paper Details

**Full Title**: "Beta Regression Framework for Modeling Bounded Biometric Performance in Child Face Recognition: A Methodological Framework with Simulation-Based Validation"

**Target Journal**: IEEE Transactions on Biometrics, Behavior, and Identity Science (T-BIOM)

**Length**: 14 pages (10 regular + 4 MOPC)

**Keywords**: Biometric evaluation, bounded outcomes, beta regression, child face recognition, longitudinal analysis, variance modeling, statistical methods

## Key Contributions

1. **Hierarchical beta regression framework** for bounded biometric performance metrics
2. **Controlled simulation** demonstrating methodological properties under known ground truth
3. **Detailed validation protocol** (Section 8.5) for real-data validation on CLF/YFA datasets
4. **Decision framework** (Table 4) for method selection
5. **Integration guidance** (Section 3.5) with ROC curves, d-prime, and DET analysis
6. **Deployment pathway** with realistic 12-18 month validation + 24-36 month pilot timeline

## Critical Finding: Boundary Violations

| Model | RMSE | R² | Invalid Predictions | Max Violation |
|-------|------|-----|-------------------|---------------|
| Linear Mixed | 0.0649 | 0.7600 | **229** | **>100%** |
| Logit-transformed | 0.0770 | 0.6620 | 0 | — |
| Beta Regression | 0.0665 | 0.7479 | **0** | — |

*Beta regression eliminates boundary violations while maintaining comparable fit (RMSE difference: 0.0016)*

## Age-Specific Patterns (from YFA study)

| Age Group | Pattern | TAR Change (6.5-8 years) |
|-----------|---------|--------------------------|
| 3-5 years | Rapid decline | 97.8% → 63.1% |
| 5.5-7 years | **Stable "Golden Window"** | 97.9% → 80.2% |
| 7.5-9 years | Delayed degradation | 98.3% → 65.6% |

*Source: Bahmani et al. (2023), Table 3*

## Simulation Details

**Synthetic data generated using:**
```python
TAR_ij = logit^(-1)(β₀ + β₁·age_i + β₂·ΔT_ij + β₃·age_i×ΔT_ij + u_i + ε_ij)
```

**Parameters calibrated to YFA patterns:**
- u_i ~ N(0, 0.15²) - between-subject variation
- ε_ij ~ N(0, 0.10²) - within-subject variability
- β₂ = -0.35 (ages 3-5: steep decline)
- β₂ = -0.08 (ages 5.5-7: stability)
- β₂ = -0.20 (ages 7.5-9: delayed degradation)
- 100 subjects per age group (300 total)
- Annual observations over 8 years

## When to Use Beta Regression

✅ **Use beta regression when:**
- Modeling population-level recognition rates (TAR/FAR) over time
- Long-term predictions (>2 years) where boundaries approached
- Variance patterns impact operational decisions
- Stakeholder communication requires interpretable percentages
- Bounded outcome interpretation essential

❌ **Do NOT use when:**
- Working with raw similarity scores (use ROC analysis)
- Individual matching decisions (use score-level methods)
- Real-time threshold adaptation needed
- Multimodal score fusion (use distributional methods)
- Algorithm development/debugging (need failure mode analysis)
- Short-term evaluations (<2 years with stable populations)

## Interactive Notebooks

| Notebook | Description | Run in Colab |
|----------|-------------|--------------|
| **BetaRegression.ipynb** | Complete statistical analysis | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/astoreyai/Dissertation/blob/main/beta-regression-framework/supplementary/notebooks/StoreyAaron_BetaRegression.ipynb) |
| **ChildFaceAnalysis.ipynb** | Data exploration & visualization | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/astoreyai/Dissertation/blob/main/beta-regression-framework/supplementary/notebooks/StoreyAaron_ChildFaceAnalysis.ipynb) |

## Quick Start

### Accessing the Research

1. **Read the Paper**:
   ```bash
   open beta-regression-framework/manuscript/paper.pdf
   ```

2. **Explore the Analysis**:
   ```bash
   cd beta-regression-framework/supplementary/notebooks/
   jupyter notebook
   ```

3. **View Key Figures**:
   ```bash
   cd beta-regression-framework/figures/
   ls *.pdf
   ```

## Ethics & Data

**Ethics Statement**: This research uses **only synthetic data** generated computationally to match published degradation patterns. No human subjects were involved. No biometric samples from real individuals were collected. IRB approval not required for purely methodological work.

**Data Sources**: Simulation parameters calibrated to:
- Bahmani et al. (2023) - Young Face Aging (YFA) dataset patterns
- Deb et al. (2018) - Children Longitudinal Face (CLF) dataset patterns

**Validation**: We actively seek collaboration with researchers who have access to CLF or YFA datasets for real-data validation.

## Validation Protocol

### Phase 1: Direct Replication
- Fit beta regression to actual TAR trajectories
- Compare boundary violations between linear and beta models
- Hypothesis: 0% violations (beta) vs 5-10% (linear)

### Phase 2: Predictive Validation
- Temporal split: train on years 0-4, test on years 5-8
- Evaluate out-of-sample accuracy and CI calibration
- Hypothesis: 95% ± 2% CI coverage

### Phase 3: Operational Validation
- Calculate re-enrollment intervals for 80% TAR threshold
- Validate age-specific recommendations
- Test demographic robustness

### Accessing Real Datasets

| Dataset | Contact | Details |
|---------|---------|---------|
| **Children Longitudinal Face (CLF)** | Deb et al. (2018) authors | 919 children, ages 2-18, 2-7 year tracking |
| **Young Face Aging (YFA)** | Bahmani et al. (2023) authors | 330 subjects, ages 3-18, 8-year tracking, 6-month intervals |

## Path to Operational Deployment

1. **Immediate (12-18 months)**: Validation on CLF/YFA datasets
2. **Medium-term (24-36 months)**: Operational pilot testing
3. **Long-term**: Integration with NCMEC search protocols

## Citation

```bibtex
@article{storey2025beta,
  title   = {Beta Regression Framework for Modeling Bounded Biometric
             Performance in Child Face Recognition: A Methodological
             Framework with Simulation-Based Validation},
  author  = {Storey, Aaron W. and Imtiaz, Masudul H.},
  journal = {IEEE Transactions on Biometrics, Behavior, and Identity Science},
  year    = {2025},
  note    = {Under review at Clarkson University for IEEE T-BIOM submission}
}
```

## Contact

**Aaron W. Storey**
Department of Computer Science
Clarkson University, Potsdam, NY 13699
storeyaw@clarkson.edu

**Masudul H. Imtiaz**
Department of Electrical & Computer Engineering
Clarkson University, Potsdam, NY 13699
mimtiaz@clarkson.edu

## License

MIT License - see [LICENSE](beta-regression-framework/LICENSE) file

## Acknowledgments

- Clarkson University for research support
- Deb et al. (2018) and Bahmani et al. (2023) for foundational datasets
- Reviewers for constructive feedback emphasizing synthetic data transparency

---

*This research contributes to reuniting missing children with their families through improved statistical modeling of biometric recognition systems.*
