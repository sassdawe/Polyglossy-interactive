# `<Program Name>` Plan

This folder contains non-invasive planning documents for `<brief purpose>` without changing existing project files.

Contents:

- `rename-surface-inventory.template.md`: Template for concrete rename surfaces discovered in the repository.
- `phased-rename-plan.template.md`: Template for a step-by-step execution plan with verification after each phase.
- `rename-dictionary.template.md`: Template for old-to-new identifier mapping and approval tracking.
- `phase-gate-checklist.template.md`: Template for command-driven validation and per-phase go/no-go records.

Planning assumptions:

- <assumption 1>
- <assumption 2>
- <assumption 3>

Recommended working order inside this folder:

1. Fill in `rename-dictionary.md` until every shipped identity has an approved replacement.
2. Use `phase-gate-checklist.md` to record the baseline and each phase's commands and pass/fail outcome.
3. Keep `phased-rename-plan.md` as the sequencing and policy source of truth.
4. Use `rename-surface-inventory.md` when a phase uncovers an untracked rename surface.

This folder is intentionally non-invasive. It is for planning and tracking only; it does not require changes to the existing product files until implementation begins.

## Suggested Deliverable Order

- Freeze the dictionary.
- Capture baseline command results.
- Execute the first phase and record the phase gate.
- Repeat for each subsequent phase.
