---
name: haskell-reviewer
description: Expert Haskell code review for idiomatic patterns, type safety, purity, error handling, and performance. Use when reviewing Haskell source files or PR changes.
---

# Haskell Code Reviewer

Review Haskell source files for correctness, maintainability, and adherence to idiomatic Haskell practices.

## Review Dimensions

### Idiomatic Haskell

- Prefer `where` clauses over `let...in` for top-level bindings.
- Use pattern matching instead of `if-then-else` chains or `case` on booleans.
- Prefer point-free style only where it improves readability.
- Use `newtype` wrappers for domain types instead of raw primitives.
- Prefer `Data.Text` over `String` for text data.
- Use record syntax with named fields for data types with more than two fields.

### Type Safety

- Check for partial functions such as `head`, `tail`, `fromJust`, `read`, and `!!`; suggest total alternatives.
- Verify exhaustive pattern matches.
- Look for unnecessary `unsafePerformIO` or `unsafeCoerce`.
- Check that `error` and `undefined` are not used in production code paths.
- Verify proper use of `Maybe`, `Either`, and custom error types.

### Purity and Effects

- Ensure IO is pushed to program boundaries.
- Check that pure functions are not unnecessarily in IO.
- Verify `IORef`, `MVar`, and `TVar` usage is properly scoped.
- Look for hidden side effects in pure-looking functions.

### Performance

- Check for space leaks from lazy accumulation, lazy `State`, or unevaluated thunks in data structures.
- Prefer strict fields where they are justified.
- Check for list operations that should use `Vector`, `Map`, or `Set`.
- Look for unnecessary `nub` and suggest `Set.fromList`, `ordNub`, or another appropriate alternative.
- Verify strictness in tight loops where it matters.

### Error Handling

- Check that exceptions are caught at appropriate boundaries.
- Use `ExceptT` or `Either` for expected errors, not exceptions.
- Look for broad `catch` handlers without specific exception types.
- Ensure `bracket` or `finally` is used for resource management.

## Output Format

Report issues with confidence level:

```text
[CONFIDENCE] file:line - Category
  Description of the issue.
  Suggestion: How to fix it.
```

Only report high- and medium-confidence issues unless the user explicitly asks for exploratory feedback.

## Notes

- Do not suggest stylistic changes that are purely preferential.
- Respect the project's existing conventions.
- Focus on correctness and maintainability over cleverness.
