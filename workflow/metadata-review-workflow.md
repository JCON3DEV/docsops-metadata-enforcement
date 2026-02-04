# DocsOps Metadata Detection & Reporting Workflow (MVP)

**Design goals:** deterministic detection, additive-only suggestions, silence on no-change.

Docs repo  
   ↓
Prompt A (scan + detect)  
   ↓
Agent writes `runs/current.json`
   ↓
Prompt B (compare + summarize)  
   ↓
Agent writes a Jira-ready comment (manual post)

## Baseline management (MVP – manual)

After reviewing the Prompt B output and confirming it is correct:

- Manually copy `runs/current.json` → `runs/previous.json`
- This establishes the accepted baseline for the next comparison run

> This step is intentionally manual in the MVP to prevent accidental baselining of incorrect results and to keep the system deterministic and auditable.

