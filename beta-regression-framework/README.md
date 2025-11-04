# Beta Regression Framework for Child Face Recognition: A Methodological Framework with Simulation-Based Validation

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Paper Status](https://img.shields.io/badge/Status-Ready%20for%20Submission-brightgreen.svg)]()

## Overview

This repository contains research addressing a critical methodological gap in child face recognition: when linear mixed models are inappropriately applied to bounded True Accept Rates (TAR), they can produce physically impossible predictions exceeding 100% accuracy. Our beta regression framework ensures mathematically valid predictions while providing superior variance modeling for operational biometric systems.

**Paper Status**: Manuscript complete and ready for IEEE T-BIOM submission (14 pages)

**Critical Finding**: In our simulation calibrated to published patterns, linear models produced 229 invalid predictions (>100% or <0%), while beta regression maintained 100% valid predictions with comparable fit (RMSE difference: 0.0016).

## Authors

**Aaron W. Storey** (Member, IEEE)
Ph.D. Candidate, Computer Science
Clarkson University, Potsdam, NY, USA
storeyaw@clarkson.edu | ORCID: 0009-0009-5560-0015

**Masudul H. Imtiaz**
Assistant Professor, Electrical & Computer Engineering
Director, AI Vision, Health, Biometrics, and Applied Computing (AVHBAC) Lab
Clarkson University, Potsdam, NY, USA
mimtiaz@clarkson.edu | ORCID: 0000-0001-5528-482X

**Sumona Mondal**
Professor of Statistics, Department of Mathematics
Co-director, MS Data Science Program
Clarkson University, Potsdam, NY, USA
smondal@clarkson.edu | ORCID: 0000-0002-0197-9148

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

## Major Additions & Revisions

### Transparency on Synthetic Data
- Title expanded to include "Simulation-Based Validation"
- Section 1.5 "Scope and Contributions" clearly states synthetic-only limitations
- Ethics statement added (no human subjects, IRB not required)
- Conditional language throughout (e.g., "2-3 years, pending validation")
- Collaboration invitation for researchers with CLF/YFA access

### Methodological Integration
- **Section 3.5**: How beta regression complements ROC/d-prime/DET methods
- **Section 10.3**: "When NOT to Use Beta Regression" (score-level analysis, individual matching, real-time adaptation, etc.)
- **Table 4**: Decision framework for practitioners
- **Table 2**: Computational performance comparison (3-5x slower than linear)

### Validation & Deployment
- **Section 8.5**: Detailed protocol with success criteria and falsification conditions
- **Section 11.5**: Path to operational deployment
- Specific dataset targets: CLF (919 children, 2-18 years), YFA (330 subjects, 8-year tracking)

## Simulation Details

Synthetic data generated using beta distribution sampling:
```
TAR_ij ~ Beta(μ_ij · φ, (1-μ_ij) · φ)
where μ_ij computed from age-specific trajectories
```

**Parameters calibrated to YFA patterns:**
- u_i ~ N(0, 0.03²) - between-subject variation
- φ = 50 - precision parameter
- β₂ = -0.35 (ages 3-5: steep decline)
- β₂ = -0.08 (ages 5.5-7: stability)
- β₂ = -0.20 (ages 7.5-9: delayed degradation)
- 100 subjects per age group (300 total)
- Annual observations over 8 years

## Age-Specific Patterns (from YFA study)

| Age Group | Pattern | TAR Change (6.5-8 years) |
|-----------|---------|-------------------------|
| 3-5 years | Rapid decline | 97.8% to 63.1% |
| 5.5-7 years | Stable period | 97.9% to 80.2% |
| 7.5-9 years | Delayed degradation | 98.3% to 65.6% |

*Source: Bahmani et al. (2023), Table 3*

## Model Comparison Results

| Model | RMSE | R² | Invalid Predictions | Max Violation |
|-------|------|-----|-------------------|---------------|
| Linear Mixed | 0.0649 | 0.7600 | 229 | >100% |
| Logit-transformed | 0.0770 | 0.6620 | 0 | None |
| Beta Regression | 0.0665 | 0.7479 | 0 | None |

*Beta regression eliminates boundary violations while maintaining comparable fit (RMSE difference: 0.0016)*

## When to Use Beta Regression

**Use beta regression when:**
- Modeling population-level recognition rates (TAR/FAR) over time
- Long-term predictions (>2 years) where boundaries approached
- Variance patterns impact operational decisions
- Stakeholder communication requires interpretable percentages
- Bounded outcome interpretation essential

**Do NOT use when:**
- Working with raw similarity scores (use ROC analysis)
- Individual matching decisions (use score-level methods)
- Real-time threshold adaptation needed
- Multimodal score fusion (use distributional methods)
- Algorithm development/debugging (need failure mode analysis)
- Short-term evaluations (<2 years with stable populations)

## Repository Structure

```
beta-regression-framework/
├── manuscript/              # IEEE T-BIOM submission (14 pages)
│   ├── paper.pdf           # Compiled manuscript (1.54 MB)
│   ├── paper.tex           # LaTeX source
│   ├── references.bib      # 31 references
│   └── compile_paper.sh    # Compilation script
├── figures/                 # All 6 publication figures
│   ├── age_patterns.pdf
│   ├── boundary_violations.pdf
│   ├── beta_regression_concepts.pdf
│   ├── variance_analysis.pdf
│   ├── prediction_intervals.pdf
│   └── operational_impact.pdf
├── supplementary/
│   ├── notebooks/          # Jupyter analysis
│   │   ├── StoreyAaron_BetaRegression.ipynb
│   │   └── StoreyAaron_ChildFaceAnalysis.ipynb
│   ├── presentations/
│   └── references/         # Bahmani 2023, Deb 2018 PDFs
├── data/                   # See data/README.md
└── README.md              # This file
```

## Interactive Notebooks

| Notebook | Description | Run in Colab |
|----------|-------------|--------------|
| **BetaRegression.ipynb** | Complete statistical analysis | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/astoreyai/beta-regression-pediatricface/blob/main/supplementary/notebooks/StoreyAaron_BetaRegression.ipynb) |
| **ChildFaceAnalysis.ipynb** | Data exploration and visualization | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/astoreyai/beta-regression-pediatricface/blob/main/supplementary/notebooks/StoreyAaron_ChildFaceAnalysis.ipynb) |

## Citation

```bibtex
@article{storey2025beta,
  title   = {Beta Regression Framework for Modeling Bounded Biometric
             Performance in Child Face Recognition: A Methodological
             Framework with Simulation-Based Validation},
  author  = {Storey, Aaron W. and Imtiaz, Masudul H. and Mondal, Sumona},
  journal = {IEEE Transactions on Biometrics, Behavior, and Identity Science},
  year    = {2025},
  note    = {Under review at Clarkson University for IEEE T-BIOM submission}
}
```

## Ethics & Data

**Ethics Statement**: This research uses only synthetic data generated computationally to match published degradation patterns. No human subjects were involved. No biometric samples from real individuals were collected. IRB approval not required for purely methodological work.

**Data Sources**: Simulation parameters calibrated to:
- Bahmani et al. (2023) - Young Face Aging (YFA) dataset patterns
- Deb et al. (2018) - Children Longitudinal Face (CLF) dataset patterns

**Validation**: We actively seek collaboration with researchers who have access to CLF or YFA datasets for real-data validation.

## Path to Operational Deployment

1. **Immediate (12-18 months)**: Validation on CLF/YFA datasets
2. **Medium-term (24-36 months)**: Operational pilot testing
3. **Long-term**: Integration with NCMEC search protocols

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

MIT License - see [LICENSE](LICENSE) file

## Acknowledgments

- Clarkson University for research support
- Deb et al. (2018) and Bahmani et al. (2023) for foundational datasets
- Reviewers for constructive feedback emphasizing synthetic data transparency

---

*This research contributes to reuniting missing children with their families through improved statistical modeling of biometric recognition systems.*
