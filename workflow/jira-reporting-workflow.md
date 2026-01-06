# Jira Reporting Workflow (MVP)

## Purpose

This document defines how metadata scan results are surfaced to humans in a
repeatable, low-noise way suitable for manual review.

The workflow is intentionally batch-oriented, deterministic, and additive-only.

## High-level flow

1. Run **Prompt A (analysis)** to scan documentation and produce a JSON result.
2. Run **Prompt B (dedupe + reporting)** to determine whether a Jira update is required.
3. Review results manually and apply metadata changes (MVP scope).
4. Preserve state for the next run.

## Inputs / Outputs (File Handoff Contract)

This workflow is file-driven and does not rely on pasted content or conversational state.

### Prompt A (Analysis)

**Output:**

- `docsops-metadata-enforcement/runs/current.json`

This file contains the full decision output for the current scan run and is the
single source of truth for detected signals, confidence, and recommendations.

### Prompt B (Deduplication + Reporting)

**Inputs:**

- `docsops-metadata-enforcement/runs/current.json`
- `docsops-metadata-enforcement/runs/previous.json` (may be missing on first run)

**Behavior:**

- If `previous.json` does not exist or is empty, Prompt B treats the run as a
  first execution and reports all relevant results.
- Prompt B compares only `decision` and `proposed_features` to determine
  meaningful change.

**Output:**

- Either:
  - `NO_CHANGES` (silent success), or
  - A single Jira-ready Markdown comment.

Prompt B never emits JSON and never requests user input.

### State rollover (MVP)

After Prompt B completes successfully:

- Copy:

```
runs/current.json → runs/previous.json
```


This is a **manual step in MVP**.
Automation may be added later once trust is established.

## Ticket creation model

- One Jira ticket per scan run
- Each ticket represents a batch review unit
- No per-file tickets

## Attached artifacts

- `runs/current.json` is attached to the Jira ticket
- JSON is treated as the canonical source of truth

## Auto-generated summary comment

- Counts per decision bucket
- Compact table for `add` and `review` items only
- No narrative justification
- Silence when no changes are detected

## Deduplication rules

- Hash = `file_path + proposed_features` (order-insensitive)
- No new comment if hashes are unchanged
- No ticket reopen on reruns

## Explicit non-goals

- No per-file Jira tickets
- No "no changes" comments
- No automated status transitions
- No metadata removals
- No license or entitlement inference

## Rationale

Batch review combined with silence-on-no-change preserves reviewer attention,
prevents alert fatigue, and builds trust in automated detection outputs.
