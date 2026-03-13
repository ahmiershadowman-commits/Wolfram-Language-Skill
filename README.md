# Wolfram-Language-Skill

A production-oriented Codex skill for building, debugging, refactoring, and auditing Wolfram Language (Mathematica) code.

## What this skill does

This skill is designed for high-quality Wolfram Language development workflows, including:

- creating new functions/packages with robust APIs;
- auditing existing code for correctness, reliability, and maintainability;
- debugging evaluation-order, pattern-matching, and scoping issues;
- improving symbolic/numeric boundary handling and performance.

## Repository layout

- `SKILL.md` — primary trigger conditions, workflow, and output expectations.
- `references/wl-build-and-refactor.md` — package architecture and refactor patterns.
- `references/wl-debugging-and-audit.md` — debugging protocol and audit rubric.
- `references/wl-performance-and-testing.md` — optimization and testing guidance.
- `examples/example-prompts.md` — realistic prompts to trigger and validate the skill.
- `examples/compact-prompt.md` — concise companion prompt for constrained contexts.

## Suggested usage

Use this skill when a request includes Wolfram Language work such as:

- “Refactor this notebook code into a package with options and tests.”
- “Why does this replacement rule loop forever?”
- “Audit this WL function for precision, memoization, and failure handling.”

## Design principles

- Explicit symbolic/numeric boundaries.
- Bounded and terminating rewrite systems.
- Structured failure signaling and option validation.
- Reproducible tests and audit-first refactor playbooks.

## Status

Current version: **0.2.0** (major documentation and workflow expansion).
