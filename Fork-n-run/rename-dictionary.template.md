# Rename Dictionary

Use this file to freeze the old-to-new identifier map before implementation starts. Do not begin code renames until all shipped identities that matter to a given phase have an approved replacement.

## Placeholder Tokens

Use neutral placeholders until the fork's branding is finalized.

- `<new-publisher>`: publisher, package owner, or organization.
- `<new-brand>`: product family name replacing old branding.
- `<new-cli-command>`: CLI or tool command replacing the old command.
- `<new-dotnet-prefix>`: .NET namespace and package prefix.
- `<new-ts-prefix>`: TypeScript or browser API prefix.
- `<new-browser-bundle>`: shipped JavaScript asset name.
- `<new-notebook-id>`: notebook type identity.
- `<new-kernel-title>`: kernel display title.

## Status Legend

- `proposed`: candidate replacement exists but is not yet approved.
- `approved`: safe to implement in the assigned phase.
- `deferred`: intentionally kept for compatibility or later cleanup.
- `legacy-alias`: old name retained temporarily after the new name ships.

## Dictionary Fields

| Old identifier | Proposed new identifier | Identifier class | Owning path or package | First change phase | Compatibility alias | Last old-name support phase | Validation proof | Status | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `Microsoft.dotnet-interactive` | `<new-dotnet-prefix>.<new-cli-command>` | artifact | `src/dotnet-interactive/dotnet-interactive.csproj` | 1 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `dotnet-interactive` | `<new-cli-command>` | artifact | `src/dotnet-interactive/dotnet-interactive.csproj` | 1 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `Microsoft.DotNet.Interactive` | `<new-dotnet-prefix>` | public API | `src/Microsoft.DotNet.Interactive/Microsoft.DotNet.Interactive.csproj` | 5 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `@microsoft/polyglot-notebooks` | `@<new-publisher>/<new-brand>-notebooks` | artifact | `src/polyglot-notebooks/package.json` | 3 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `microsoft.dotnet.interactive.js` | `<new-brand>.interactive.js` | artifact | `src/polyglot-notebooks-browser/package.json` | 3 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `dist/dotnet-interactive.js` | `dist/<new-browser-bundle>` | artifact | `src/polyglot-notebooks-browser/package.json` | 3 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `createDotnetInteractiveClient` | `create<new-ts-prefix>Client` | public API | `src/polyglot-notebooks-browser/src/library-init.ts` | 7 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `getDotnetInteractiveScope` | `get<new-ts-prefix>Scope` | public API | `src/polyglot-notebooks-browser/src/library-init.ts` | 7 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `dotnet-interactive-vscode` | `<new-brand>-interactive-vscode` | artifact | `src/polyglot-notebooks-vscode/package.json` | 3 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `ms-dotnettools` | `<new-publisher>` | artifact | `src/polyglot-notebooks-vscode/package.json` | 3 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `Polyglot Notebooks` | `<new-brand> Notebooks` | artifact | `src/polyglot-notebooks-vscode/package.json` | 3 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `Microsoft Corporation` | `<new-publisher>` | artifact | `src/polyglot-notebooks-vscode/package.json` | 3 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `ms-dotnettools.dotnet-interactive-vscode` | `<new-publisher>.<new-brand>-interactive-vscode` | persisted ID | `src/polyglot-notebooks-vscode/package.json` | 9 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `dotnet-interactive.acquire` | `<new-notebook-id>.acquire` | persisted ID | `src/polyglot-notebooks-vscode/package.json` | 9 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `dotnet-interactive.kernelTransportArgs` | `<new-notebook-id>.kernelTransportArgs` | persisted ID | `src/polyglot-notebooks-vscode/package.json` | 9 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `dotnet-interactive.notebookParserArgs` | `<new-notebook-id>.notebookParserArgs` | persisted ID | `src/polyglot-notebooks-vscode/package.json` | 9 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `dotnet-interactive.kernelTransportWorkingDirectory` | `<new-notebook-id>.kernelTransportWorkingDirectory` | persisted ID | `src/polyglot-notebooks-vscode/package.json` | 9 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `dotnet-interactive.interactiveToolSource` | `<new-notebook-id>.interactiveToolSource` | persisted ID | `src/polyglot-notebooks-vscode/package.json` | 9 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `dotnet-interactive.minimumDotNetSdkVersion` | `<new-notebook-id>.minimumDotNetSdkVersion` | persisted ID | `src/polyglot-notebooks-vscode/package.json` | 9 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `dotnet-interactive.requiredInteractiveToolVersion` | `<new-notebook-id>.requiredInteractiveToolVersion` | persisted ID | `src/polyglot-notebooks-vscode/package.json` | 9 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `onNotebook:dotnet-interactive` | `onNotebook:<new-notebook-id>` | persisted ID | `src/polyglot-notebooks-vscode/package.json` | 9 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `dotnet-interactive` | `<new-notebook-id>` | persisted ID | `src/polyglot-notebooks-vscode/package.json` | 9 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `dotnet-interactive-window` | `<new-notebook-id>-window` | persisted ID | `src/polyglot-notebooks-vscode/package.json` | 9 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `polyglot-notebook` | `<new-brand>-notebook` | persisted ID | `src/polyglot-notebooks-vscode/package.json` | 9 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `polyglot-notebook-window` | `<new-brand>-notebook-window` | persisted ID | `src/polyglot-notebooks-vscode/package.json` | 9 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `.NET Interactive (C#)` | `<new-kernel-title> (C#)` | persisted ID | `src/polyglot-notebooks-vscode/package.json` | 9 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `.NET Interactive (F#)` | `<new-kernel-title> (F#)` | persisted ID | `src/polyglot-notebooks-vscode/package.json` | 9 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `.NET Interactive (PowerShell)` | `<new-kernel-title> (PowerShell)` | persisted ID | `src/polyglot-notebooks-vscode/package.json` | 9 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |
| `dotnet tool run dotnet-interactive -- notebook-parser` | `dotnet tool run <new-cli-command> -- notebook-parser` | persisted ID | `src/polyglot-notebooks-vscode/package.json` | 9 | `<yes/no/optional>` | `<phase-or-n/a>` | `<command-or-scenario>` | `proposed` | `<notes>` |

## Approval Checklist

Before a row changes from `proposed` to `approved`, confirm all of the following.

- The replacement does not use restricted or trademark-bearing product identity.
- The replacement matches the fork's naming convention across affected platforms and documentation.
- The first-change phase is consistent with [phased-rename-plan.md](./phased-rename-plan.md).
- Compatibility intent is explicit for any client-server or persisted-state seam.
- There is at least one command or scenario that proves the new name works.

## Review Notes

- Do not guess final names in code from this file until legal or product naming is approved.
- Add rows whenever a new shipped identity is discovered in [rename-surface-inventory.md](./rename-surface-inventory.md).
- Keep deferred legacy aliases in this file until they are intentionally removed.
