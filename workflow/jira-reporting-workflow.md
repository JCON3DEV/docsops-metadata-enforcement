# Jira Reporting Workflow (MVP)

## Purpose

This document explains how metadata scan results are surfaced to humans without creating noise.

## Ticket creation model

- One ticket per scan run
- Ticket represents a batch review unit

## Attached artifacts

- Full JSON output attached as the source of truth

## Auto-generated summary comment

- Counts per decision bucket
- Compact table for add/review items only
- No prose justification

## Deduplication rules

- Hash = file_path + proposed_features
- No new comment if unchanged
- No ticket reopen on reruns

## Explicit non-goals

- No per-file tickets
- No "no changes" comments
- No automated status transitions

## Rationale

Reviewing results in batches and remaining silent when nothing changes prevents noise and maintains reviewer trust.
