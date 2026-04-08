---
description: 'Cost estimation guidance for infrastructure, CI/CD, dependency, and tooling changes with plausible spend impact'
applyTo: '**'
excludeAgent: []
---
# Cost Estimation Instructions

Guidance for reviewing changes that can plausibly alter operating cost, especially infrastructure, CI/CD, dependency, and paid tooling updates.

## When To Use

- Reviewing a PR or diff that changes infrastructure, deployment, build, or workflow configuration
- Reviewing dependency or tooling changes that could affect paid usage, licensing, compute time, storage, or SaaS seats

## Guidance

### Identify Credible Cost Drivers

- Start by isolating changed files and lines that can directly change spend, such as instance sizing, autoscaling thresholds, storage classes, retention periods, runner selection, build frequency, artifact uploads, or paid service enablement
- Distinguish direct cost drivers from indirect code changes; do not speculate unless the diff shows a concrete mechanism that would change usage or billing
- Treat dependency and tooling changes as cost-relevant only when they introduce or expand paid services, larger runtime footprints, additional build work, or license changes with pricing implications

### Source Pricing Data

- Prefer Infracost when the changed infrastructure is supported and the repository provides enough context to generate a meaningful estimate
- When Infracost is unavailable or incomplete, use current public pricing pages, pricing calculators, or primary vendor documentation
- Record where each number came from and include the pricing date or retrieval date when the source is time-sensitive
- If pricing differs by region, environment size, runner class, or usage volume, state the ambiguity and use a range instead of a single-point estimate

### Show the Estimate Clearly

- Show the calculation path so a reviewer can reproduce the estimate from the diff and cited pricing inputs
- Report estimates in USD with both per-day and per-month views; use a simple 30-day month unless the source provides a more appropriate billing basis
- Avoid false precision; round to a sensible level and explain the main assumptions that drive uncertainty
- If only part of the impact can be estimated, separate the estimated portion from any unquantified risk

### Keep the Review Focused

- Do not add a dedicated "no cost impact" section or zero-dollar table when the diff contains no credible cost-related changes
- If the review contains other findings, simply omit cost commentary when there is no cost signal
- If the requested task is solely a cost-impact review and no credible cost-related changes are present, use a brief statement that no estimate was produced because no cost-relevant change was found

## Validation Checklist

- [ ] Every estimate is tied to a specific changed file or configuration change
- [ ] Pricing inputs are sourced from Infracost output or current public pricing documentation
- [ ] Assumptions and ambiguities are stated explicitly
- [ ] Daily and monthly estimates are shown for each quantified change
- [ ] No filler no-impact section or unsourced zero estimate was added
