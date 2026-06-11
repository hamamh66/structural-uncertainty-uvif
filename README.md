# Decision-Making Under Structural Uncertainty

**Structural uncertainty estimator and UVIF-based decision policy for robust decision-making under distribution shift.**

This repository supports the manuscript:

> *Decision-Making Under Structural Uncertainty: An Experimental Validation of the Unified Variational Intelligence Framework*

The project introduces and tests a decision-centric method for detecting when a model class itself becomes unreliable under distribution shift. Instead of treating uncertainty only as aleatoric noise or epistemic parameter uncertainty, the framework estimates **structural uncertainty**: the model--reality gap caused by hypothesis-class misspecification.

---

## Repository link title

Suggested GitHub repository name:

```text
structural-uncertainty-uvif
```

Suggested repository URL:

```text
https://github.com/habibhamam/structural-uncertainty-uvif
```

---

## Short description

Structural uncertainty estimation and UVIF-based decision-making under distribution shift, with synthetic validation, falsification controls, and decision-level evaluation for abstention and hedging.

---

## What this repository contains

This repository is intended to contain the code, data-processing scripts, result tables, and figures needed to reproduce the experimental validation of the proposed Structural-Uncertainty Decision Model (SUDM).

The current companion notebook implements **Tier A**, the controlled synthetic protocol in which the true model--reality gap is known by construction.

Expected repository structure:

```text
structural-uncertainty-uvif/
├── README.md
├── notebooks/
│   └── tierA_structural_uncertainty.ipynb
├── manuscript/
│   └── Decision_Making_Under_Structural_Uncertainty.pdf
├── results/
│   ├── tables/
│   └── figures/
├── src/
│   ├── structural_decomposition.py
│   ├── decision_policy.py
│   └── evaluation_metrics.py
└── requirements.txt
```

---

## Core idea

Standard uncertainty quantification usually separates uncertainty into:

- **Aleatoric uncertainty**: irreducible noise in the data-generating process.
- **Epistemic uncertainty**: uncertainty caused by limited data and reducible with more observations.

This project adds a third component:

- **Structural uncertainty**: the gap between reality and the best model attainable inside a chosen hypothesis class.

The paper operationalizes this structural component through a hierarchical predictive-disagreement decomposition:

```text
Total predictive disagreement = within-class disagreement + between-class disagreement
```

where:

- `Varwithin` is used as an epistemic proxy.
- `Varbetween` is used as a structural-uncertainty proxy.

The key claim is that under distribution shift, the between-class term grows when different model classes extrapolate differently, revealing model-class inadequacy that ordinary within-class uncertainty estimators may miss.

---

## Decision model

The structural-uncertainty signal is not used only as a diagnostic score. It is integrated into a UVIF-derived decision objective:

```text
J_dec(a | x) = E[L_task(a, x)] + beta R_tail(a, x) + eta Var_between(x)
```

The resulting policy may:

- commit to an action,
- hedge the decision,
- abstain,
- or trigger a regime-level alarm when structural shift becomes too large.

---

## Experiments

### Tier A: Controlled synthetic validation

The synthetic environment is designed so that the true structural error is known. This allows the method to test whether `Varbetween` tracks the true model--reality gap.

The Tier A notebook evaluates:

- **H1**: Structural uncertainty improves decision cost under shift.
- **H2**: Between-class disagreement tracks true structural error better than within-class disagreement.
- **H3**: The structural advantage increases with shift magnitude.
- **H4a**: The advantage disappears when all model classes are well specified.
- **H4b**: A homogeneous ensemble cannot reproduce the structural signal.

### Tier B: Real-data validation

The manuscript also evaluates short-term electricity-transformer forecasting under seasonal regime shift. The structural signal rises with seasonal distance, while within-class uncertainty remains comparatively flat.

---

## Main outputs

The experiments generate:

- mechanism-validation plots,
- risk--coverage curves,
- dose--response curves,
- falsification-control plots,
- AURC and decision-cost tables,
- structural and epistemic uncertainty summaries.

---

## Installation

Create a Python environment and install the required packages:

```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

A minimal environment should include:

```bash
pip install numpy pandas scipy matplotlib scikit-learn jupyter
```

---

## Running the Tier A notebook

```bash
jupyter notebook notebooks/tierA_structural_uncertainty.ipynb
```

The notebook trains heterogeneous model classes, computes the within-class and between-class components, compares them against the ground-truth structural error, and evaluates the UVIF structural decision policy under increasing shift.

---

## Reproducibility notes

The notebook uses fixed random seeds where possible. Because some estimators include stochastic optimization, small numerical variations may occur across platforms.

Recommended practice:

- keep the same Python and scikit-learn versions across runs,
- store generated tables in `results/tables/`,
- store generated figures in `results/figures/`,
- record all final hyperparameters in the notebook or in a configuration file.

---

## Suggested citation

```bibtex
@misc{hamam2026structuraluncertaintyuvif,
  title  = {Decision-Making Under Structural Uncertainty: An Experimental Validation of the Unified Variational Intelligence Framework},
  author = {Hamam, Habib},
  year   = {2026},
  note   = {Code and supplementary materials},
  url    = {https://github.com/habibhamam/structural-uncertainty-uvif}
}
```

---

## License

A license should be added before public release. Suggested options:

- **MIT License** for code reuse.
- **CC BY 4.0** for documentation, figures, and supplementary text.

---

## Contact

Prof. Habib Hamam  
Faculty of Engineering, Université de Moncton  
Email: Habib.Hamam@umoncton.ca
