---
name: haskell-build
description: Build a Haskell project, interpret GHC errors, and apply safe fixes. Use when the user asks Codex to build Haskell code, fix compilation errors, or run cabal/stack build workflows.
---

# Haskell Build Workflow

Build the current Haskell project, parse GHC errors, and attempt automatic fixes when the cause is clear.

## Steps

1. Detect the build tool by checking for `cabal.project`, `stack.yaml`, or `*.cabal` files in the workspace.
2. Run `cabal build` or `stack build`, passing along any user-supplied build arguments.
3. If the build succeeds, report success and stop.
4. If the build fails, parse GHC diagnostics for file paths, line numbers, and error messages.
5. Group errors by file, read the relevant code, and apply focused fixes.
6. Re-run the build after edits, up to three iterations when progress is being made.
7. If errors remain, report the remaining diagnostics and the safest next manual fix.

## Fix Strategy

- Type mismatch: inspect expected and actual types, then fix signatures, conversions, or call sites.
- Not in scope: check imports and module exports before adding imports or qualification.
- Parse error: check indentation, missing `do`, malformed `where`, and layout-sensitive syntax.
- Redundant constraint: remove constraints only when GHC clearly proves they are unused.
- Missing instance: prefer deriving clauses for lawful standard instances; avoid hand-written instances unless needed.

## Notes

- Preserve the project's existing code style and indentation.
- Do not remove user comments or documentation.
- If a fix is ambiguous or could change behavior, explain the tradeoff before editing.
