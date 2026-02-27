---
description: 'Scaffold a new Architecture Decision Record (ADR) with proper structure and numbering.'
agent: 'agent'
tools:
  - 'editFiles'
---

# Create ADR

Create a new Architecture Decision Record (ADR) for a technical or process decision.

## Instructions

1. **Determine the next ADR number** by checking existing files in `docs/dev/adrs/` (or the project's ADR directory). Use the format `ADR-NNN`.

2. **Create the ADR file** at `docs/dev/adrs/ADR-NNN-${input:slug:short-kebab-case-title}.md` with this structure:

```markdown
# ADR-NNN: ${input:title:Decision title}

## Status

Proposed

## Context

<!-- What is the issue that we're seeing that is motivating this decision or change? -->

## Decision

<!-- What is the change that we're proposing and/or doing? -->

## Consequences

### Easier

<!-- What becomes easier or possible as a result of this change? -->

### More Difficult

<!-- What becomes more difficult as a result of this change? -->

## Alternatives Considered

<!-- What other options were evaluated? Why were they rejected? -->

## References

<!-- Links to related ADRs, documentation, or external resources -->
```

1. **Fill in the Context section** based on the user's description of the problem.

2. **Leave Decision, Consequences, and Alternatives as prompts** unless the user has already articulated the decision.

3. **Update the ADR index** if one exists (e.g., `docs/dev/adrs/README.md`).
