# MVP Scope Guardrails

This document defines the **explicit scope boundaries** for the metadata enforcement MVP.

These guardrails exist to:

- Prevent scope creep
- Protect trust in automation
- Keep the MVP evaluable and reversible

Anything not listed here is **out of scope by default**.


## In scope

The MVP supports the following capabilities only:

### Detection

- Scan documentation files for **explicit, contract-defined hard signals**
- Evaluate signals against the taxonomy contract
- Produce a deterministic, machine-readable decision output

### Reporting

- Report detected signals, confidence scores, and proposed metadata
- Surface human-verifiable evidence (snippets and line numbers)
- Support review workflows via structured output

### Metadata actions

- **Additive suggestions only**
- No automated removals
- No automated overwrites


## Out of scope

The MVP explicitly does **not** support:

- Machine learning or probabilistic inference
- Heuristic or fuzzy matching
- Automatic metadata removals
- Badge rendering or UI behavior
- License or entitlement inference
- Editorial interpretation or marketing positioning
- Real-time or continuous enforcement
- Cross-repository enforcement


## Execution model

- Execution is **manual or ad hoc**
- Expected cadence: **quarterly** or as-needed
- Single reviewer model (documentation owner)
- Output is treated as advisory unless explicitly approved


## Automation constraints

Automation is permitted **only** when all of the following are true:

- Confidence meets or exceeds the auto-add threshold
- No taxonomy contract constraints are violated
- Signals are explicit and unambiguous
- The proposed change is additive

If any condition fails, the system must defer to human review.


## Change management

Changes to any of the following require re-baselining:

- Taxonomy contract
- Hard-signal dictionary
- Confidence thresholds
- Gold set

Silent changes are not permitted.


## Exit conditions

This MVP is intentionally temporary.

The MVP must be retired, replaced, or re-scoped when:

- A formal, platform-wide taxonomy redesign is implemented, or
- Metadata ownership is transferred to a centralized system of record, or
- Automation requirements exceed the constraints defined here

Target sunset: **2026 taxonomy redesign**.


## Summary

This MVP prioritizes:

- Correctness over coverage
- Determinism over intelligence
- Reversibility over optimization

The purpose is not to automate faster, but to automate **safely**.
