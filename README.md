
# African Brain Age

Reproducible neuroimaging-based brain age estimation with a focus on African data generalizability.

**African Neurodata Research Lab (ANR Lab)**  
Brain Age Estimation Project

---

## Project goal

Build a clean, reproducible pipeline that:

1. Learns normal age-related patterns from healthy T1-weighted MRI
2. Predicts brain age on unseen scans
3. Computes Brain Age Gap (BAG)
4. Applies proper age-bias correction
5. Tests accuracy, calibration and fairness — especially on African MRI data

Most existing brain-age models are trained mainly on Western or majority-population datasets. This project examines how well such models (and models we train ourselves) transfer to African neuroimaging data, with transparent reporting of where they succeed and where they fail.

> Core research question:  
> Do brain-age models trained mainly on international datasets remain accurate, calibrated and fair when applied to African MRI data?

---

## Phase 1 scope

- **Modality**: T1-weighted structural MRI only
- **Training target**: Chronological age in neurologically healthy / cognitively normal participants
- **Modelling route**: Feature-based machine learning baseline first (Elastic Net / Ridge, SVR, tree/boosting models)
- **Public cohorts used for normative training**: OpenBHB → OASIS-3 → additional datasets as needed
- **African / Nigerian data**: Reserved primarily for external validation, fairness analysis and local benchmarking
- **Out of scope for first release**: Clinical diagnosis claims, individual patient “brain age” reports, training large 3D CNNs from scratch on small data

---

## Current status

| Dataset   | Role                          | Status              |
|-----------|-------------------------------|---------------------|
| OpenBHB   | Multi-site healthy controls   | Filtering complete  |
| OASIS-3   | Older cognitively normal      | Metadata exploration starting |
| Dataset 3 | TBD                           | Pending             |
| Nigerian Clinical MRI | External validation / fairness | Planned             |

OpenBHB filtering produced two manifests:
- **Strict** (target scanner families only)
- **Relaxed** (target families + Siemens Tim Trio)

---

## Repository structure

```
african-brain-age/
├── notebooks/
│   ├── OpenBHB_Filtering.ipynb
│   └── OASIS3_Filtering.ipynb
├── manifests/                  # filtered subject lists and audit trails
├── docs/                       # decisions, protocols, handoff notes
├── config/                     # model and pipeline configuration (later)
└── README.md
```

Large MRI files and controlled-access participant data are **not** stored in this repository. GitHub is used for code, manifests, documentation and provenance only.

---

## High-level pipeline

```
Public + African MRI sources
        ↓
Metadata-first filtering (healthy / normal, 3T, scanner rules)
        ↓
Selective image download
        ↓
Standardized preprocessing (FreeSurfer / CAT12 or equivalent)
        ↓
Feature extraction
        ↓
Feature-based age prediction models
        ↓
Brain Age Gap + age-bias correction
        ↓
External validation & fairness analysis on African data
```

---

## Key principles

- Participant-level splitting (no leakage across train/validation/test)
- All learned steps fitted on training data only
- Full audit trail for inclusions, exclusions and QC failures
- Both raw and bias-corrected BAG are reported
- Results broken down by age, sex, diagnosis and site where sample size allows
- Research tool only — not a diagnostic product

---

## Team

- **Joseph Duruh** – Research Assistant, project lead on data strategy and scientific framing
- **Angelic Charles** – Computational Engineer, model and pipeline implementation
- **African Neurodata Research Lab**

---

## References (selected)

- Cole & Franke (2017). Predicting age using neuroimaging: innovative brain ageing biomarkers.
- Kumari et al. (2024). Review of brain age prediction models.
- Treder et al. (2021); Zhang et al. (2023); Kalc et al. (2024) — age-bias correction.
- Wogu et al. (2025) — FAIR African brain data and Nigerian Clinical-MRI dataset.
- OpenBHB, OASIS-3, ADNI, UK Biobank, HCP-Aging documentation.

---

## License & data use

Code in this repository is for research use.  
All source datasets remain under their original data-use agreements and licenses. Users must obtain their own access approvals (e.g. OASIS DUA, NITRC, etc.).
```

