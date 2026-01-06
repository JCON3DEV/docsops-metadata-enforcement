---
title: Taxonomy Contract Real-Time Customer Data Platform
description: Temporary enforcement contract defining valid RTCDP edition and package metadata, including allowed combinations, defaults, and detection constraints for metadata enforcement MVP automation.
---
# Decision output schema

Required fields:

file_path
current_features[]            # existing metadata on the page (input state)

signals_matched[]             # array of signal hits
  - rule_id
  - signal_type
  - match_pattern
  - weight

evidence[]                    # human-verifiable proof
  - snippet
  - line_number

proposed_features[]           # features suggested by the system (additive only)

confidence                    # numeric, derived from weighted signals

decision                      # system recommendation
  - add        # safe to auto-add
  - review     # human required
  - ignore     # no action

decision_rationale            # 1–2 sentences, machine-generated, deterministic

constraints_violated[]        # optional, populated only if contract rules block auto-add
