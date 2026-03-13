# Example Prompts

Use these prompts to exercise all major skill pathways.

## Build mode
- Build a Wolfram Language package that computes graph centrality metrics with `OptionsPattern[]`, input validation, and `VerificationTest` coverage.
- Create a symbolic simplifier pipeline with three explicit stages and bounded rewriting.

## Refactor mode
- Refactor this notebook cell dump into a package with public/private contexts and usage messages.
- Split this 300-line function into normalized input parsing, transformation, and rendering components.

## Audit mode
- Audit this WL code for evaluation-order bugs and UpValue collisions; provide a severity-ranked findings table.
- Review this mixed symbolic/numeric workflow for precision leaks and exact arithmetic blowups.

## Debug mode
- My `//.` rewrite never terminates for nested expressions. Diagnose and fix with a bounded approach.
- Why does this rule work in one notebook but fail in a fresh kernel? Provide a state-isolation diagnosis.
