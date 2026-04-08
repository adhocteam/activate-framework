---
description: 'Estimate the cost impact of infrastructure, CI/CD, dependency, or tooling changes in a PR or branch diff.'
agent: 'agent'
tools:
  - 'changes'
  - 'fetch_webpage'
  - 'run_in_terminal'
  - 'github'
  - 'codebase'
---
# Cost Impact Review

Review a change set for credible cost impact. Focus on infrastructure, CI/CD, dependency, and tooling changes with a direct or clearly explainable spend implication.

## Instructions

1. Determine the review target from the user's request before analyzing any changes:
   - If the user specifies an open PR by number or URL, review that PR.
   - Otherwise, if active PR context is available, review the current PR.
   - Otherwise, compare the current branch against `main`.
2. Inspect the changed files and identify only the changes that can plausibly alter spend, such as infrastructure sizing, scaling, storage, network egress, runner class, artifact retention, build frequency, paid tooling usage, or dependency/license changes with clear cost implications.
3. Prefer Infracost when the changed infrastructure is supported and the repository provides enough context. If Infracost cannot produce a reliable estimate, use current public pricing pages or other primary vendor pricing documentation.
4. Show the calculation path for every quantified estimate. Include the changed configuration, the pricing input, the usage assumption, and the arithmetic that leads to the estimate.
5. Report cost impact in USD with both per-day and per-month figures. Use a range when region, workload, usage volume, or configuration details are ambiguous.
6. State ambiguities plainly. If the diff suggests a possible cost change but key pricing inputs are missing, explain why the estimate is partial or uncertain.
7. Do not invent cost findings. If there are no credible cost-related changes:
   - omit a dedicated no-impact section when the response contains other review content; or
   - if this is a standalone cost review, return a brief statement that no estimate was produced because no cost-relevant changes were found.
8. Cite the source for each pricing input and include the date the pricing data was retrieved when relevant.
9. Keep the final result easy to scan.

## Output Format

When cost-relevant changes exist, produce:

- A short verdict summarizing the overall expected cost direction and confidence
- A table with: change, evidence, cost driver, estimate per day, estimate per month, range or confidence notes
- A "Show Your Work" section with the calculation steps and assumptions for each finding
- A "Sources" section with the pricing references used
- An "Ambiguities" section only when uncertainty materially affects the estimate

When no credible cost-relevant changes exist and this is a standalone cost review, produce a brief statement that no estimate was produced because the reviewed changes do not show a direct cost mechanism.

## Context

If a `cost-estimation.instructions.md` file exists in `.github/instructions/`, follow that guidance in addition to the workflow above.
