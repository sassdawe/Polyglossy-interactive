# Phased Rename Plan

This plan assumes the fork or product will adopt a new neutral brand and execute renames in waves, validating after each wave before moving on.

## Goals

- <goal 1>
- <goal 2>
- <goal 3>
- <goal 4>

## Naming Strategy Before Any Code Change

Pick and freeze the replacement vocabulary first. Do not start renaming until the replacement map is agreed and written down.

Minimum required map:

- organization or publisher prefix
- core product or engine name
- CLI or tool command
- extension ID and display name
- .NET root namespace prefix
- TypeScript or browser symbol prefix
- package scope and package name replacements
- notebook type IDs and kernel titles

Deliverable before implementation:

- one rename dictionary mapping every old public identifier to its replacement

Recommended fields in the rename dictionary:

- old identifier
- new identifier
- identifier class: artifact, public API, runtime protocol, persisted ID, or docs-only
- owning path or package
- first phase in which it changes
- whether a compatibility alias is required
- last phase in which the old name is still supported
- validation command or test proving the new name works

## Cross-Phase Operating Rules

These rules keep the rename effort attributable and reversible.

1. Change only one identity layer per phase.
2. Do not combine artifact renames and public API renames in the same commit unless a clean build is otherwise impossible.
3. For any rename that crosses a client-server seam, prefer a dual-name compatibility window for one phase.
4. Treat persisted IDs differently from source names.
5. Do not sweep docs and samples during runtime phases unless they are needed as test fixtures.
6. Every phase must end with a branch state that can be tagged and used as a recovery point.

## Compatibility Policy

Not every old name needs a compatibility shim. Use this policy to decide.

Keep compatibility temporarily for:

- tool command names consumed by another component
- browser globals consumed by shipped content
- command IDs and settings keys stored in user configuration
- notebook type IDs and kernelspec IDs that may already exist in user content

Do not prioritize compatibility for:

- internal file names with no runtime lookup
- internal class names not used in serialization, reflection, or generated contracts
- docs-only strings

Preferred compatibility mechanisms by surface:

- .NET public API: type forwarders, compatibility namespaces, wrapper entry points
- TypeScript public API: re-export old names, keep old globals as delegating aliases
- extension: accept both old and new settings or commands for one migration window
- CLI/tooling: transitional wrapper script or alias if required for cutover

## Rollback and Hold Criteria

Stop after the current phase and do not continue if any of the following is true.

- <hold criterion 1>
- <hold criterion 2>
- <hold criterion 3>
- <hold criterion 4>

For each phase, record:

- exact commit hash at phase start
- exact commit hash at phase pass
- known regressions accepted into the next phase
- explicit decision to proceed or hold

## Phase 0. Baseline and Safety Net

Objective: establish a reproducible baseline before any rename.

Steps:

1. Record the current failing and passing baseline for build and tests.
2. Build the smallest solution or package slice needed for the first phase.
3. Run relevant frontend or package tests.
4. Run highest-value backend or integration tests.
5. Run manual end-to-end flows that represent expected user behavior.
6. Save the baseline command list and outcomes.

Validation gate:

- You have a known-good command set for later phase comparisons.
- Any existing failures are documented as pre-existing and are not mistaken for rename regressions.

Deliverables:

- baseline command log
- baseline pass/fail matrix
- frozen rename dictionary draft

## Phase 1. Rename Artifact Identities

Objective: rename package IDs, assembly names, project file names, solution entries, tool identity, bundle names, or other artifact identities without yet renaming public APIs.

Scope:

- `<path-or-package>`
- `<path-or-package>`
- `<path-or-package>`

Rules for this phase:

- Keep runtime/API shim compatibility where possible.
- Do not rename namespaces or public type names yet unless required for a clean build.
- Prefer temporary aliases/shims over simultaneous API churn.

Concrete work items:

1. Rename project, package, or artifact file names and references.
2. Rename package IDs, assembly names, root namespaces, or bundle outputs only where needed for artifact identity.
3. Rename CLI or tool command identities.
4. Update build, packaging, solution, and artifact output references.
5. Update dependent defaults only if the artifact change must be consumed immediately for verification.

Validation gate:

- build affected solution or package slice
- focused tests for packaging-sensitive paths
- smoke test the renamed tool, package, or artifact
- manual end-to-end verification if another component consumes the artifact

Exit criteria:

- artifacts can be built and invoked under the new names
- no public API rename has been attempted beyond what this phase strictly needs

## Phase 2. Verify End-to-End After Artifact Rename

Objective: prove the product still works with the new artifact identities before touching public APIs.

Steps:

1. Point dependent components at locally built renamed artifacts.
2. Run the primary manual scenario.
3. Execute startup, switching, save/open, and cross-component scenarios.
4. Run integration tests available on the machine.
5. Confirm parser, registration, or acquisition paths still invoke the correct executable or package.

Validation gate:

- startup works
- parser or registration operations work
- resource loading still works
- no hardcoded old artifact assumption blocks startup

## Phase 3. Rename Secondary Artifact Identities

Objective: rename remaining package, extension, browser, or distributable artifact identities without yet renaming public APIs.

Scope:

- `<path-or-package>`
- `<path-or-package>`
- `<path-or-package>`

Concrete work items:

1. Rename package names and descriptions.
2. Rename extension or distributable metadata as needed.
3. Rename display branding that is artifact identity only.
4. Rename generated bundle output if applicable.
5. Keep backward-compatible command/config aliases temporarily if installed-user migration matters.

Validation gate:

- install dependencies, compile, and test each affected package
- distributable packages can be built locally
- renamed resources are still embedded, served, or consumed correctly

Exit criteria:

- package and distributable identities reflect the new branding
- public symbols remain unchanged unless strictly necessary

## Phase 4. Verify End-to-End After Secondary Artifact Rename

Objective: confirm that packaging and startup still work after the secondary artifact rename wave.

Steps:

1. Install or point to the locally built distributable.
2. Configure dependent settings to the renamed local artifact if not already defaulted.
3. Re-run the primary manual scenario.
4. Run common/client tests for affected packages.
5. Run contract tests for shipped bundles or generated artifacts.

Validation gate:

- distributable installs under new identity
- activation or startup events still fire
- commands/settings still resolve correctly
- renamed resources load correctly

## Phase 5. Rename Public APIs and Namespaces

Objective: rename namespaces, public type names, and public runtime APIs after artifact stability is already proven.

Why this is separated:

- this is often the widest source-compatibility change
- it can impact tests, samples, generated code, loaders, reflection, and package consumers

Concrete work items:

1. Rename namespaces and public API prefixes.
2. Rename assembly-qualified references, reflection lookups, and extension entry points.
3. Regenerate any generated outputs that depend on renamed types.
4. Update package references and imports across tests and samples as needed.
5. Decide whether to ship temporary compatibility namespaces or type forwarders.
6. Review serializers, diagnostics, resource names, and string-based type references for old values.

Validation gate:

- full build for affected tree
- focused tests for public API and runtime behavior
- generated contract tests
- manual scenarios that exercise extension loading or public APIs

Exit criteria:

- runtime code builds under the new namespace or API family
- generated artifacts and entry points agree with the new names

## Phase 6. Verify End-to-End After Public API Rename

Objective: catch hardcoded cross-boundary expectations before touching additional client-side or persisted identifiers.

Most likely failure points in this phase:

- generated interface or contract mismatches
- resource lookups still using old embedded names
- registration metadata assuming old IDs
- transport/config code still constructing old command lines
- tests or startup code using reflection over old namespaces

Validation gate:

- rerun the primary manual workflow
- rerun contract tests
- rerun registration or startup checks
- confirm startup, execution, sharing, and parser operations still behave correctly

## Phase 7. Rename Client Public APIs and Contracts

Objective: rename browser globals, channel interfaces/classes, exported client names, and other client public symbols after the server or runtime API side is stable.

Scope examples:

- `<old-client-symbol>`
- `<old-client-symbol>`
- `<old-client-symbol>`

Concrete work items:

1. Rename client symbols in source.
2. Rename mirrored client symbols across package copies if applicable.
3. Update tests first where possible to expose remaining old-name assumptions.
4. Consider temporary compatibility exports/globals for one migration window.
5. Update resource references if the bundle name also changes in this phase.
6. Keep old browser globals delegating to new names until the final ID cleanup phase unless explicitly breaking compatibility.

Validation gate:

- client package tests
- core package tests
- common tests in affected package copies
- manual workflow covering browser/client APIs

Exit criteria:

- client public APIs no longer expose the old naming
- client/server protocol remains intact

## Phase 8. Verify End-to-End After Client API Rename

Objective: prove the final client-side rename wave did not silently break runtime protocol assumptions.

Checks:

1. Install local distributable and run the primary manual scenario again.
2. Verify startup, switching, completions, diagnostics, explorer views, parser actions, and save/open.
3. Verify browser or client output features backed by the shipped client library.
4. Re-run available browser or integration tests.

## Phase 9. Rename Persisted IDs, Commands, Settings, and Migration Shims

Objective: clean up the last layer of externally visible IDs after runtime halves are already operating under the new brand.

Scope:

- command IDs
- configuration keys
- notebook type IDs and activation events
- kernel or registration IDs and display names
- marketplace/package references in docs and tests

Why last:

- these IDs are often persisted in user settings and user content
- changing them early creates avoidable install/upgrade friction while runtime code is still moving

Recommended tactic:

- support old and new IDs in parallel for one transition window where practical
- log deprecation warnings before removing the old names

Migration work items:

1. Introduce new settings keys and command IDs.
2. Read old settings keys as fallback.
3. Register old and new commands to the same handler during the migration window.
4. Support old notebook type or kernel IDs where the hosting platform allows it.
5. Remove the old IDs only after at least one stable internal pass of the complete workflow.

Validation gate:

- existing content still opens
- new content uses only new IDs
- settings migration works or is clearly documented
- registration uses new IDs and titles

## Phase 10. Documentation, Samples, and Cleanup

Objective: sweep the broad but lower-risk surfaces only after product/runtime identities are stable.

Scope:

- `README.md`
- `docs/**`
- `samples/**`
- notebooks, screenshots, marketplace links, package references, badges, and troubleshooting text

Validation gate:

- spot-check samples with the renamed tool/package identities
- docs no longer instruct users to install or reference old fork-specific names

Deliverables:

- final rename dictionary marked complete
- migration notes for downstream consumers
- explicit list of intentionally retained legacy aliases, if any

## Suggested Validation Matrix by Phase

## Reusable Phase-Gate Record

Capture this for every phase:

- scope changed
- compatibility shims added
- automated commands run
- manual end-to-end scenarios run
- pass/fail result
- rollback point
- go/no-go decision

## After Runtime or Backend Phases

- build projects touched in that phase
- targeted tests for CLI, transport, registration, browser, or integration paths
- local tool invocation smoke test

## After Client or Frontend Phases

- package compile command
- package test command
- browser or client contract tests
- common tests for mirrored package copies

## After Every Major Wave

- local distributable install
- primary manual walkthrough
- parser or save/open test
- startup test with locally built dependent components together

## Hardcoded Expectation Hotspots to Audit Early

These are the places most likely to fail if one side moves before the other.

- config defaults that shell out to an old command
- browser global names in client initialization code
- embedded resource names and server-side file provider lookups
- tests asserting extension, kernel, or package IDs
- activation events using old persisted IDs
- generated interface contracts between generators and consumers
- documentation or samples used as manual smoke tests that still assume old names

## Persisted-State Hotspots

These need migration attention, not just source renaming.

- user settings under old configuration keys
- installed registration metadata
- notebook or file metadata containing language IDs or notebook type markers
- approved or snapshot test files pinning old IDs and asset names
- CI or release artifact naming that downstream automation depends on

## Suggested Commit Structure

Keep commits attributable to the rename wave.

1. preflight baseline and rename dictionary
2. first artifact rename
3. end-to-end verification after first artifact rename
4. secondary artifact rename
5. end-to-end verification after secondary artifact rename
6. public API rename
7. end-to-end verification after public API rename
8. client API rename
9. end-to-end verification after client API rename
10. persisted IDs, settings migration, docs, and cleanup

## Final Acceptance Criteria

The rename effort is complete only when all of the following are true.

- no shipped package, extension, tool, browser global, or public API uses old restricted identity without an explicit reason
- the local tool, local distributable, parser flow, and primary workflow all pass together
- registration works with the new IDs
- bundle loading and client contracts are stable under the new names
- docs and samples point only to the new identity
- any retained compatibility aliases are documented with an explicit removal phase or are intentionally permanent

## Recommended Execution Discipline

For each phase:

1. rename one identity layer only
2. build the smallest affected slice immediately
3. run the narrowest automated tests that can disconfirm the phase
4. run at least one end-to-end smoke test before continuing
5. only then widen to the next identity layer
