# Rename Surface Inventory

This inventory groups the concrete rename surfaces that will need attention when removing or replacing shipped identifiers.

## 1. Artifact Identity Surfaces

These are packaging, assembly, project, command, bundle, or release identifiers that flow into build outputs or published artifacts.

- `<path-or-package>`
  - `<identifier-name>`: `<current-value>`
  - `<identifier-name>`: `<current-value>`

## 2. Public API and Namespace Surfaces

These affect consumers, source compatibility, reflection, serialization, generated code, and tests.

- `<namespace-or-api-pattern>`
- `<using-or-import-pattern>`
- `<entry-point-or-contract-name>`

## 3. TypeScript Package and Browser API Surfaces

These are TypeScript, JavaScript, browser global, package, and distributable asset identifiers.

- `<package-or-file-path>`
  - package name: `<current-value>`
  - exported symbol: `<current-value>`
  - global symbol: `<current-value>`

## 4. Extension Identity Surfaces

These affect extension installation, upgrade behavior, commands, settings, activation events, notebook type IDs, and marketplace continuity.

- `<extension-package-path>`
  - extension name: `<current-value>`
  - display name: `<current-value>`
  - publisher: `<current-value>`
  - command IDs:
    - `<command-id>`
  - configuration keys:
    - `<configuration-key>`

## 5. Notebook, Kernel, and Parser Identity Surfaces

These are cross-boundary IDs that can break if client and server code stop agreeing.

- notebook activation and notebook type IDs:
  - `<notebook-type-id>`
- kernel display titles:
  - `<kernel-title>`
- parser command wiring:
  - `<parser-command>`

## 6. Cross-Boundary Resource and Protocol Surfaces

These are places most likely to break when one side is renamed before the other.

- resource name: `<resource-name>`
- browser global contract: `<global-name>`
- generated contract: `<contract-name>`
- transport or configuration seam: `<seam-name>`

## 7. Automated Validation Surfaces Already Present

These existing tests are useful as safety rails during phased renames.

- `<test-project-or-package>`
- `<test-file-or-suite>`
- `<manual-scenario-file>`

## 8. Documentation and Sample Surfaces

These are broad but mechanically simpler once code identities are stable.

- `<docs-path>`
- `<samples-path>`
- `<repository-metadata-path>`

## 9. Planned Rename Order Rationale

Recommended ordering is based on blast radius:

1. `<identity-layer-1>`: `<rationale>`
2. `<identity-layer-2>`: `<rationale>`
3. `<identity-layer-3>`: `<rationale>`
4. `<identity-layer-4>`: `<rationale>`
5. `<identity-layer-5>`: `<rationale>`
