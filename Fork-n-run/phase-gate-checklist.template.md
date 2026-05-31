# Phase Gate Checklist

Use this file as the execution record for the rename program. Each phase should capture the exact commands run, the manual scenarios exercised, the rollback point, and the go or hold decision.

## Baseline Command Set

Record the current state before any rename work starts.

Baseline commit recorded for Phase 0 preparation: `<commit-hash>`.

### Root and Backend Baseline

| Command | Expected purpose | Result | Notes |
| --- | --- | --- | --- |
| `<command>` | `<expected-purpose>` | `<not-run/passed/failed/skipped>` | `<notes>` |

### Frontend or Package Baseline

| Working directory | Command | Expected purpose | Result | Notes |
| --- | --- | --- | --- | --- |
| `<working-directory>` | `<command>` | `<expected-purpose>` | `<not-run/passed/failed/skipped>` | `<notes>` |

## Manual End-to-End Checklist

Run this sequence after each verification phase.

1. Install or point the app, extension, or host at the local build.
2. Configure transport, parser, package, or runtime settings to local artifacts if the current phase changed command paths or IDs.
3. Open the primary manual scenario file or start the primary workflow.
4. Start the runtime successfully.
5. Execute representative language, feature, or integration scenarios.
6. Verify cross-component data sharing or protocol behavior.
7. Verify package loading, acquisition, registration, or extension-specific flow if the phase affected it.
8. Save and reopen any persisted content.
9. Verify parser-backed or format conversion open/save behavior if the phase touched parser or notebook IDs.
10. Record whether any step still depends on an old name.

Phase 0 manual end-to-end results should be recorded below. Run this checklist again before and after any phase that changes tool paths, notebook IDs, parser IDs, extension acquisition behavior, or persisted identifiers.

## Phase 0 Preparation Record

- Scope changed:
- Compatibility aliases added:
- Rollback commit:
- Proceed or hold:

### Phase 0 Commands Run

- Command:
  - Expected purpose:
  - Result:
  - Notes:

### Phase 0 Manual End-to-End Result

- Startup:
  - Result:
  - Notes:

- Representative execution:
  - Result:
  - Notes:

- Cross-component behavior:
  - Result:
  - Notes:

- Save and reopen:
  - Result:
  - Notes:

- Parser or format flow:
  - Result:
  - Notes:

- Acquisition, registration, or install flow:
  - Result:
  - Notes:

### Phase 0 Stop Conditions Triggered

- None or list triggered hold criteria from [phased-rename-plan.md](./phased-rename-plan.md).

## Per-Phase Gate Template

Copy this block for each phase execution.

### Phase X Record

- Scope changed:
- Compatibility aliases added:
- Rollback commit:
- Proceed or hold:

#### Commands Run

- Command:
  - Expected purpose:
  - Result:
  - Notes:

- Command:
  - Expected purpose:
  - Result:
  - Notes:

#### Manual End-to-End Result

- Startup:
  - Result:
  - Notes:

- Representative execution:
  - Result:
  - Notes:

- Cross-component behavior:
  - Result:
  - Notes:

- Save and reopen:
  - Result:
  - Notes:

- Parser or format flow:
  - Result:
  - Notes:

- Acquisition, registration, or install flow:
  - Result:
  - Notes:

#### Stop Conditions Triggered

- None or list triggered hold criteria from [phased-rename-plan.md](./phased-rename-plan.md).

## Recommended Command Set by Phase

### Phase 1 and Phase 2: First Artifact Rename and Verification

- `<build-command>`
- `<focused-test-command>`
- `<integration-test-command>`
- run the renamed CLI or artifact with a smoke-test command
- run the manual end-to-end checklist

### Phase 3 and Phase 4: Secondary Artifact Rename and Verification

- in `<package-or-working-directory>`: `<compile-command>` and `<test-command>`
- in `<package-or-working-directory>`: `<compile-command>` and `<test-command>`
- build local distributables
- run the manual end-to-end checklist

### Phase 5 and Phase 6: Public API Rename and Verification

- repeat the focused build and test set from Phase 1
- add generator regeneration and dependent tests if applicable
- rerun integration tests because string-based type references may move
- run the manual end-to-end checklist

### Phase 7 and Phase 8: Client API Rename and Verification

- repeat the focused compile and test set from Phase 3
- pay special attention to browser/client package tests for renamed globals and exports
- rerun manual scenarios that exercise client APIs

### Phase 9 and Phase 10: Persisted IDs, Docs, and Cleanup

- rerun the manual end-to-end checklist with existing content and newly created content
- rerun registration or persisted-ID tests
- verify settings migration using old and new config keys
- spot-check docs and samples after cleanup

## Go or Hold Rules

Mark the phase as `hold` immediately if any of the following occurs.

- The local distributable cannot start the primary workflow with local artifacts.
- A resource can no longer be discovered by its host.
- Registration or parser flow breaks because IDs or executable names drifted.
- A compatibility alias is required but not yet implemented.
- A persisted-state change would strand existing settings or content without fallback.

Do not move to the next phase until the current phase record shows:

- all required commands run
- manual end-to-end results recorded
- rollback commit captured
- explicit `proceed` decision
