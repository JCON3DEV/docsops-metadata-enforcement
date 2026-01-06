# Feature badge mapping (RTCDP)

This document defines the **authoritative mapping** between RTCDP metadata features and their corresponding UI badges.

The purpose of this mapping is to **decouple taxonomy from presentation** so that:

- Metadata enforcement remains stable
- UI rendering can evolve independently
- Badge drift does not silently corrupt metadata semantics

This file is **reference-only** in the MVP and is not consumed by automation.


## Scope

This mapping applies only to:

- RTCDP edition features
- RTCDP tier features (Prime / Ultimate)

It does **not** define:

- Badge rendering behavior
- Badge placement rules
- UI visibility logic
- Eligibility or entitlement rules

Those concerns live outside this contract.


## Governing rules

- Every badge must map to **exactly one** metadata feature
- Badge keys are treated as **UI identifiers**, not taxonomy values
- Metadata features remain the system of record
- Badge presence must never imply a feature that is not explicitly tagged


## Canonical feature-to-badge mapping

| Feature | Badge key | Label | Type | Canonical URL |
|-------|----------|------|------|---------------|
| RTCDP B2B | `badgeB2B` | B2B Edition | Informative | https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html |
| RTCDP B2C | `badgeB2C` | B2C Edition | Informative | https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html |
| RTCDP B2P | `badgeB2P` | B2P Edition | Informative | https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html |
| RTCDP Prime | `badgePrime` | Prime | Informative | https://helpx.adobe.com/legal/product-descriptions.html |
| RTCDP Ultimate | `badgeUltimate` | Ultimate | Informative | https://helpx.adobe.com/legal/product-descriptions.html |


## Reference JSON representation (non-authoritative)

The following JSON snippet illustrates how this mapping could be represented for machine use.
It is **not** normative in the MVP.

```json
{
  "RTCDP B2B": {
    "badge_key": "badgeB2B",
    "label": "B2B Edition",
    "type": "Informative",
    "url": "https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html"
  },
  "RTCDP B2C": {
    "badge_key": "badgeB2C",
    "label": "B2C Edition",
    "type": "Informative",
    "url": "https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html"
  },
  "RTCDP B2P": {
    "badge_key": "badgeB2P",
    "label": "B2P Edition",
    "type": "Informative",
    "url": "https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html"
  },
  "RTCDP Prime": {
    "badge_key": "badgePrime",
    "label": "Prime",
    "type": "Informative",
    "url": "https://helpx.adobe.com/legal/product-descriptions.html"
  },
  "RTCDP Ultimate": {
    "badge_key": "badgeUltimate",
    "label": "Ultimate",
    "type": "Informative",
    "url": "https://helpx.adobe.com/legal/product-descriptions.html"
  }
}
```


## Change control

Any change to this mapping:

- Requires review alongside the taxonomy contract
- Must not introduce new feature semantics
- Must preserve backward compatibility where possible

This mapping exists to **prevent drift**, not to enable experimentation.
