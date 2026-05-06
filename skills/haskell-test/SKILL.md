---
name: haskell-test
description: Run and interpret Haskell test suites. Use when the user asks Codex to run HSpec, QuickCheck, Tasty, cabal test, stack test, or diagnose failing Haskell tests.
---

# Haskell Test Workflow

Run HSpec, QuickCheck, or Tasty tests for the current Haskell project and summarize the result clearly.

## Steps

1. Detect the build tool by checking for `cabal.project`, `stack.yaml`, or `*.cabal` files.
2. If the user provides a module name, test name, or pattern, pass it through using the project's normal test-filtering mechanism.
3. Run `cabal test` or `stack test`.
4. Parse the output for passed, failed, and pending tests.
5. For each failure, extract the test name, expected and actual values, counterexamples, and source location when available.
6. Read the relevant test and source files to identify whether the failure is in implementation, assumptions, or test data.
7. Suggest or apply fixes according to the user's request and the confidence of the diagnosis.

## Notes

- Do not modify test files unless the user asks or the test is clearly wrong.
- Preserve QuickCheck counterexamples, especially shrunk minimal cases.
- If no test suite exists, suggest a small HSpec/Tasty setup that matches the project.
