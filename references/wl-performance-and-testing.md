# WL Performance and Testing Reference

## Performance workflow
1. Establish baseline with representative inputs.
2. Measure wall time and memory for hot functions.
3. Identify symbolic simplification hotspots.
4. Introduce targeted changes; remeasure.
5. Keep a short regression benchmark suite.

## Common optimization levers
- Replace repeated `Simplify` with precomputed assumptions and narrower transforms.
- Prefer structural transforms to full algebraic simplification when possible.
- Memoize pure deterministic subproblems with bounded key spaces.
- Compile numeric kernels when expression structure is stable and numeric-only.
- Avoid repeated conversion between exact and approximate numbers.

## Testing strategy
- Unit tests for normalization and option validation.
- Property-style checks for invariants (idempotence, monotonicity, conserved quantities).
- Golden tests for canonical formatting/serialization.
- Regression tests for previously observed WL edge cases.

## `VerificationTest` template
```wl
Needs["MUnit`"];

TestReport @ {
  VerificationTest[
    myFunction[{1,2,3}],
    <|1 -> 1, 2 -> 2, 3 -> 3|>,
    TestID -> "normalizes list input"
  ],
  VerificationTest[
    FailureQ @ myFunction["bad"],
    True,
    TestID -> "rejects invalid input"
  ]
}
```

## Documentation expectations
- One-line usage for each public function.
- Option table with defaults and accepted values.
- At least one symbolic example and one numeric example.
- “Failure modes” section for actionable user recovery.
