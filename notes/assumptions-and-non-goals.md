# Assumptions and Non-Goals: Edition and Tier Metadata

This document captures the **explicit assumptions** and **deliberate exclusions** that govern how editions and tiers are represented in metadata for this MVP.

These decisions are intentional and contract-driven, not accidental omissions.


## Assumption: How RTCDP is commercially structured

Adobe Real-Time Customer Data Platform (RTCDP) is sold using two orthogonal dimensions:

### Editions (what kind of CDP)

- B2C
- B2B
- B2P

Editions define **structural differences**, including:

- Core data models (people vs. accounts)
- Domain concepts (for example, Businessperson Profiles vs. Consumer Profiles)
- Supported workflows and use cases
- UI surfaces and terminology

### Tiers (how much of that edition is licensed)

- Prime
- Ultimate

Every RTCDP customer is licensed on **exactly one tier**.
There is no "free", "basic", or "edition-only" license.

Commercially, this means:

> RTCDP = Edition × (Prime OR Ultimate)


## Non-Goal: License inference through documentation metadata

Although every customer has a tier, this MVP **does not infer tier metadata** unless the documentation explicitly requires it.

This is a deliberate separation between:

- **Sales reality** (all customers have a tier)
- **Documentation responsibility** (only assert what the content guarantees)

### Documentation rule (contractual)

Tier metadata is applied **only when content is explicitly tier-gated**, such as:

- A feature that does not exist in Prime
- A capability that is blocked or unavailable without Ultimate

If a feature:

- Exists in both Prime and Ultimate, or
- Has different quantitative limits by contract, or
- Uses language such as "you can purchase more"

→ The documentation remains **tier-neutral**, and no tier metadata is applied.

Tagging in these cases would require guessing, which this system explicitly avoids.


## Observation: Why RTCDP documentation often appears ambiguous

Adobe documentation frequently:

- States availability at the **edition** level
- Describes limits or guardrails
- Mentions upsell paths without naming tiers explicitly

This pattern reflects intentional product positioning:

- The feature exists across tiers
- The scale differs by contract
- The documentation avoids over-specifying commercial terms

As a result:

- Edition tagging is usually correct and stable
- Tier tagging must be rare and explicit


## Governing mental model for this MVP

- **Edition metadata**
  - Common
  - Structural
  - High confidence
  - Safe to automate when explicit

- **Tier metadata**
  - Rare
  - Entitlement-specific
  - Explicit only
  - Never inferred from limits or pricing language

If the documentation does not force a Prime or Ultimate distinction:

> The system must not invent one.


## Summary

Every RTCDP customer has a tier, but not every document is allowed to say which one.

This constraint is intentional and foundational to the MVP. It exists to prevent metadata drift, protect downstream automation, and preserve trust in machine-consumed documentation.
