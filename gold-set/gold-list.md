# Gold Set: RTCDP Metadata Calibration List

This gold set is a **small, hand-labeled reference set** used to calibrate detection thresholds and validate metadata decisions during the MVP phase.

It is intentionally minimal.  
The goal is **signal tuning**, not coverage.

## Usage rules

- Files are selected to represent:
  - Obvious edition-specific content
  - Obvious generic content
  - Ambiguous or mixed cases
- Labels reflect **expected metadata only**, not current repo state.
- No prose justification is included.
- This list is not exhaustive and is not intended to grow large.

## Gold list

| file_path | expected_features | safe_to_auto_add |
|----------|-------------------|------------------|
| `help/rtcdp/b2b-overview.md` | `RTCDP B2B` | yes |
| `help/dashboards/data-models/cdp-insights-data-model-b2c.md` | `RTCDP B2C` | yes |
| `help/rtcdp/overview.md` | `RTCDP B2B, RTCDP B2P, RTCDP B2C, RTCDP Prime, RTCDP Ultimate` | yes |
| `help/segmentation/methods/flexible-audience-evaluation.md` | `RTCDP B2C` | yes |
| `help/destinations/catalog/social/linkedin-b2b.md` | `RTCDP B2B` | yes |
| `help/destinations/guardrails.md` | *(none)* | no |
| `help/destinations/catalog/advertising/branch.md` | *(none)* | no |
| `help/data-governance/mtls-api/overview.md` | *(none)* | no |
| `help/data-governance/e2e.md` | *(none)* | no |
| `help/catalog/datasets/experience-event-dataset-retention-ttl-guide.md` | `RTCDP B2B, RTCDP Prime, RTCDP Ultimate` | yes |
| `help/dashboards/home.md` | *(none)* | no |
| `help/landing/home.md` | *(none)* | no |
| `help/landing/api-guide.md` | *(none)* | no |
| `help/identity-service/home.md` | *(none)* | no |
| `help/query-service/data-distiller/derived-datasets/overview.md` | *(none)* | no |

## Notes

- `(none)` indicates intentionally generic content.
- `safe_to_auto_add = yes` means the expected features could be applied automatically **if detected at high confidence**.
- This list must be revisited if the taxonomy contract changes.
