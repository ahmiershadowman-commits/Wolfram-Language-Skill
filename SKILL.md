---
name: wolfram-language-engineer
description: Use this skill when users ask to design, implement, debug, refactor, optimize, document, or audit Wolfram Language (Mathematica) code, notebooks, packages, or paclets. Covers symbolic programming patterns, evaluation semantics, numeric workflows, testing, and code-quality review.
---

# Wolfram Language Engineer

## Purpose
Use this skill to deliver production-quality Wolfram Language work across three common modes:
1. **Build**: create new functions, packages, notebooks, or paclet-ready components.
2. **Refactor**: improve readability, modularity, API design, and maintainability.
3. **Audit**: review correctness, robustness, performance, and developer ergonomics.

## Trigger cues
Activate this skill when the request includes:
- Wolfram Language / Mathematica / `.wl` / `.wls` / `.nb` / paclet development.
- Symbolic transformation rules, pattern matching, UpValues/DownValues, or evaluation-order issues.
- Numeric and mixed symbolic-numeric tasks (NDSolve, optimization, linear algebra, fitting, etc.).
- Requests to debug scoping, assumptions, precision, recursion, memoization, or nontermination.

## Response modes
Before implementation, infer or ask for one of these modes:
- **Fast fix**: minimal safe patch and short explanation.
- **Production**: polished API, options, validation, tests, and docs.
- **Audit-first**: issue report first, then prioritized remediation.

Default to **Production** unless the user explicitly asks for quick iteration.

## Core workflow

### 1) Clarify intent and constraints
Capture:
- expected inputs/outputs and invariants;
- symbolic vs numeric guarantees;
- scale/performance targets;
- notebook-only vs package/paclet destination.

If uncertain, make explicit assumptions and proceed.

### 2) Choose representation boundaries
Define where each stage happens:
- parsing/normalization;
- symbolic transformation;
- numeric realization;
- formatting/export.

Do not mix stages casually; this prevents evaluation leaks and rewrite blowups.

### 3) Implement with WL-safe patterns
Prefer:
- clear contexts and public/private split for packages;
- `OptionsPattern[]` with typed option validation;
- explicit failure contracts (`Failure[...]`, messages, `$Failed` mapping policy);
- local scoping (`Module`, `Block`, `With`) chosen intentionally;
- bounded and terminating rewrite systems.

Avoid brittle global state and accidental value capture.

### 4) Validate and test
Always include:
- nominal examples;
- edge cases (empty, missing, malformed, large, symbolic/numeric mixed);
- at least one failure-path test;
- deterministic behavior checks where order/evaluation matters.

Prefer `VerificationTest`/`TestReport` for package code.

### 5) Audit and harden
Run an explicit pass for:
- performance hotspots;
- precision and exact-arithmetic explosions;
- memoization growth/lifetime;
- UpValue collisions and context pollution;
- notebook hidden state dependencies.

## Debugging stance (WL-specific)
When debugging, inspect in this order:
1. **Evaluation semantics**: `Hold*` attributes, delayed vs immediate rules, unintended evaluation.
2. **Pattern specificity**: overly broad patterns, missing conditions, precedence pitfalls.
3. **Rule termination**: oscillating rewrites, unbounded `ReplaceRepeated`.
4. **Scope/state**: symbol leakage, stale definitions, notebook execution order.
5. **Numeric stability**: precision tracking, machine vs arbitrary precision mismatch.

Useful probes include `Trace`, `TraceScan`, `FullForm`, `Definition`, `DownValues`, `UpValues`, and lightweight timing/memory checks.

## Robustness patterns

### Input and option validation
- Validate shape/type early; fail loudly with actionable messages.
- Normalize equivalent forms (e.g., scalar/list/association variants) once at boundaries.
- Keep internal forms stable to reduce branch complexity.

### Failure signaling
- Use structured `Failure` payloads for machine-readable diagnostics.
- Include remediation hints in messages.
- Keep success/failure return conventions consistent across the API.

### Rewrite discipline
- Prefer finite, staged transformations over monolithic global rewrite passes.
- Add guards (`Condition`/`PatternTest`) to prevent overmatching.
- Use explicit max-iteration bounds where repeated rewriting is necessary.

### Numeric discipline
- Introduce numerics intentionally (`N`, `SetPrecision`) at clear points.
- Avoid exact arithmetic in high-degree / high-dimension operations unless required.
- Use assumptions and domains to constrain simplification.

## Refactor & audit playbook
For existing code, produce:
1. **Findings table**: issue, severity, evidence, impact.
2. **Refactor plan**: ordered patches with risk level.
3. **Implementation**: smallest safe sequence of changes.
4. **Verification**: before/after tests and behavior notes.

High-value refactors:
- split public API from kernel internals;
- replace implicit globals with explicit parameters/options;
- extract repeated rule fragments into named transforms;
- convert notebook-only logic into package functions.

## Package and paclet progression
When asked to “flesh out” solutions:
1. Start with standalone function prototypes.
2. Move to package layout with usage messages and tests.
3. Add examples and migration notes.
4. Optionally package as a paclet once API stabilizes.

## Output expectations
Unless user requests otherwise, return:
- concise rationale;
- complete WL code block(s);
- tests/examples;
- known limitations and next improvements.

For audits, include prioritized recommendations (P0/P1/P2).

## Reference files
Load only as needed:
- `references/wl-build-and-refactor.md` for implementation and architecture patterns.
- `references/wl-debugging-and-audit.md` for diagnostic checklists and failure modes.
- `references/wl-performance-and-testing.md` for optimization and validation strategy.
