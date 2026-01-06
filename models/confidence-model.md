# Confidence Model (MVP)

This document defines how detected hard signals are translated into **actionable decisions** during the MVP phase.

The model is intentionally simple, deterministic, and auditable.


## Definition

**Confidence score** is calculated as:


Only signals defined in the **Hard-Signal Dictionary** contribute to confidence.

No inference, decay, or normalization is applied in the MVP.


## Thresholds

| Confidence range | Decision |
|-----------------|----------|
| ≥ 0.75 | Auto-add candidate |
| 0.40 – 0.74 | Needs review |
| < 0.40 | Ignore |


## Enforcement rules

- **Auto-add**
  - Allowed only when confidence ≥ 0.75
  - Must also pass all taxonomy contract constraints
- **Review**
  - Requires human validation
  - No automated metadata changes
- **Ignore**
  - No action taken
  - No reporting noise generated


## Explicit constraints

- Metadata removals are **never automated** in the MVP.
- Confidence scoring does not override taxonomy contract violations.
- Ambiguity is treated as a signal to defer, not to infer.


## Rationale

This model prioritizes:

- Low noise over high recall
- Deterministic behavior over probabilistic guessing
- Human trust over automation coverage

The model is expected to evolve only after the taxonomy contract and signal dictionary are proven stable.
