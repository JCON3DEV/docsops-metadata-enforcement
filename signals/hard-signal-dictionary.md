---
title: Hard-Signal Dictionary
description: Canonical, detection-only dictionary of explicit hard signals used to identify RTCDP edition- and tier-specific documentation content for MVP metadata enforcement. Signals are intentionally restrictive, deterministic, and contract-derived.
---
# Hard-Signal Dictionary (v0.2)

**Scope:** MVP metadata enforcement — detection only  
**Derivation:** Strict implementation of Taxonomy Contract Sections 5 and 7  
**Inference:** None  
**ML:** None  
**Rule count:** 12 (intentionally capped)


## Global Signal Constraints (Non-Negotiable)

These constraints apply to **all rules** below:

- **Signal surface (MVP):**
  - Scan **document body and headings only**
  - **Do NOT** treat front matter as evidence
  - **Do NOT** treat `keywords`, badges, or navigation labels as evidence
- **Front matter usage:**
  - Front matter is read **only** to extract `current_features`
- **Proposed features MUST be canonical:**
  - `RTCDP B2B`
  - `RTCDP B2C`
  - `RTCDP B2P`
  - `RTCDP Prime`
  - `RTCDP Ultimate`
- **Absence of signals is expected and valid**


## Edition Signals

### Rule B2B-01 — Explicit B2B Edition Reference

- **rule_id:** `b2b_explicit_edition`
- **applies_to:** `RTCDP B2B`
- **signal_type:** `explicit_string`
- **match_pattern:**  
  `Real[- ]?Time Customer Data Platform \(?B2B Edition\)?|Real[- ]?Time CDP \(?B2B Edition\)?`
- **confidence_weight:** `0.7`
- **exclusions:** none


### Rule B2B-02 — Businessperson Profile (Standalone)

- **rule_id:** `b2b_businessperson_profile`
- **applies_to:** `RTCDP B2B`
- **signal_type:** `explicit_string`
- **match_pattern:**  
  `Businessperson Profile(s)?`
- **confidence_weight:** `0.6`
- **exclusions:**
  - pages explicitly scoped to `RTCDP B2P`


### Rule B2B-03 — Account + Businessperson Profile Coupling

- **rule_id:** `b2b_account_profile_with_businessperson`
- **applies_to:** `RTCDP B2B`
- **signal_type:** `explicit_string`
- **match_pattern:**  
  `Account Profile(s)?.{0,200}Businessperson Profile(s)?|Businessperson Profile(s)?.{0,200}Account Profile(s)?`
- **confidence_weight:** `0.6`
- **exclusions:**
  - `RTCDP B2P`
  - `Consumer Audience`


### Rule B2C-01 — Explicit B2C Edition Reference

- **rule_id:** `b2c_explicit_edition`
- **applies_to:** `RTCDP B2C`
- **signal_type:** `explicit_string`
- **match_pattern:**  
  `Real[- ]?Time Customer Data Platform \(?B2C Edition\)?|Real[- ]?Time CDP \(?B2C Edition\)?`
- **confidence_weight:** `0.7`
- **exclusions:** none


### Rule B2C-02 — Consumer Audience

- **rule_id:** `b2c_consumer_audience`
- **applies_to:** `RTCDP B2C`
- **signal_type:** `explicit_string`
- **match_pattern:**  
  `Consumer Audience(s)?`
- **confidence_weight:** `0.5`
- **exclusions:**
  - `Business Audience`
  - `Businessperson Profile`


### Rule B2P-01 — Explicit B2P Edition Reference

- **rule_id:** `b2p_explicit_edition`
- **applies_to:** `RTCDP B2P`
- **signal_type:** `explicit_string`
- **match_pattern:**  
  `Real[- ]?Time Customer Data Platform \(?B2P Edition\)?|Real[- ]?Time CDP \(?B2P Edition\)?`
- **confidence_weight:** `0.7`
- **exclusions:** none


### Rule B2P-02 — Dual Profile Model (Person + Businessperson)

- **rule_id:** `b2p_dual_profile_model`
- **applies_to:** `RTCDP B2P`
- **signal_type:** `explicit_string`
- **match_pattern:**  
  `Person Profile(s)?.{0,200}Businessperson Profile(s)?|Businessperson Profile(s)?.{0,200}Person Profile(s)?`
- **confidence_weight:** `0.6`
- **exclusions:** none


## Edition Entitlement Constraints

> These rules detect **explicit availability restrictions** that limit a feature or capability
> to a specific RTCDP edition.
>
> They apply **regardless of placement** in the document body (including notes, footnotes,
> and callouts), but only when restriction language is explicit and unambiguous.
>
> These rules are intentionally high-precision and **do not infer intent**.

### Rule B2B-ENT-01 — Explicit B2B Availability Restriction

- **rule_id:** `b2b_entitlement_only`
- **applies_to:** `RTCDP B2B`
- **signal_type:** `entitlement_phrase`
- **match_pattern:**  
  `(only|available only|required|requires|limited)(.{0,40})(B2B Edition|RTCDP B2B)`
- **confidence_weight:** `0.75`
- **exclusions:**
  - pages explicitly scoped to `RTCDP B2P`


### Rule B2C-ENT-01 — Explicit B2C Availability Restriction

- **rule_id:** `b2c_entitlement_only`
- **applies_to:** `RTCDP B2C`
- **signal_type:** `entitlement_phrase`
- **match_pattern:**  
  `(only|available only|required|requires|limited)(.{0,40})(B2C Edition|RTCDP B2C)`
- **confidence_weight:** `0.75`
- **exclusions:**
  - pages explicitly scoped to `RTCDP B2P`


### Rule B2P-ENT-01 — Explicit B2P Availability Restriction

- **rule_id:** `b2p_entitlement_only`
- **applies_to:** `RTCDP B2P`
- **signal_type:** `entitlement_phrase`
- **match_pattern:**  
  `(only|available only|required|requires|limited)(.{0,40})(B2P Edition|RTCDP B2P)`
- **confidence_weight:** `0.75`
- **exclusions:** none


<!--
NON-SIGNALS (Intentional)

The following language patterns are explicitly NOT treated as entitlement signals
and must not trigger edition tagging:

- "Designed for B2B use cases"
- "Commonly used in B2B scenarios"
- "Typically used by B2B customers"
- "Works best for B2B"
- "Supports B2B workflows"

These phrases are descriptive or advisory, not contractual availability constraints.
Treating them as signals would introduce inference and reduce trust in the system.
-->


## Package (Tier) Signals

> Tier signals apply **only when explicitly and unambiguously stated**.  
> Quantitative limits, quotas, or "you can purchase more" language are **not valid signals**.

### Rule PRIME-01 — Explicit Prime Product Naming

- **rule_id:** `prime_explicit_product_name`
- **applies_to:** `RTCDP Prime`
- **signal_type:** `explicit_string`
- **match_pattern:**  
  `Real[- ]?Time Customer Data Platform Prime|Real[- ]?Time CDP Prime`
- **confidence_weight:** `0.6`
- **exclusions:** none


### Rule PRIME-02 — Prime Collaboration Credit Entitlement

- **rule_id:** `prime_collaboration_2500`
- **applies_to:** `RTCDP Prime`
- **signal_type:** `entitlement_phrase`
- **match_pattern:**  
  `2,500 Collaboration Credits`
- **confidence_weight:** `0.6`
- **exclusions:**
  - `5,000 Collaboration Credits`


### Rule ULT-01 — Explicit Ultimate Product Naming

- **rule_id:** `ultimate_explicit_product_name`
- **applies_to:** `RTCDP Ultimate`
- **signal_type:** `explicit_string`
- **match_pattern:**  
  `Real[- ]?Time Customer Data Platform Ultimate|Real[- ]?Time CDP Ultimate`
- **confidence_weight:** `0.6`
- **exclusions:** none


### Rule ULT-02 — Destination SDK Hard Gate

- **rule_id:** `ultimate_destination_sdk_entitlement`
- **applies_to:** `RTCDP Ultimate`
- **signal_type:** `entitlement_phrase`
- **match_pattern:**  
  `Access to (the )?Destination SDK|Destination SDK enabling Customer to build custom destination connectors`
- **confidence_weight:** `0.6`
- **exclusions:** none


## Contract-Violation Detectors (Non-Additive)

> These rules **never add features**.  
> They exist solely to block auto-add when the taxonomy contract is violated.

### Rule VIO-01 — Prime and Ultimate Coexistence

- **rule_id:** `invalid_prime_and_ultimate_coexist`
- **applies_to:** `RTCDP Prime|RTCDP Ultimate`
- **signal_type:** `feature_name`
- **match_pattern:**  
  front matter contains both `RTCDP Prime` **and** `RTCDP Ultimate`
- **confidence_weight:** `0.7`
- **exclusions:** none


### Rule VIO-02 — Package Without Edition

- **rule_id:** `invalid_package_without_edition`
- **applies_to:** `RTCDP Prime|RTCDP Ultimate`
- **signal_type:** `feature_name`
- **match_pattern:**  
  front matter contains `RTCDP Prime` or `RTCDP Ultimate` **without** one of:
  - `RTCDP B2B`
  - `RTCDP B2C`
  - `RTCDP B2P`
- **confidence_weight:** `0.7`
- **exclusions:** none


## Implementation Notes (Read This)

- Signals are **necessary but never sufficient** on their own
- Confidence scoring does **not** override taxonomy constraints
- Tier tagging is intentionally **rare**
- Silence is a success state
- Any new rule must:
  1. Trace to the taxonomy contract
  2. Survive false-positive analysis
  3. Justify its operational cost

This dictionary is optimized for **trust, restraint, and long-term maintainability**, not coverage.
