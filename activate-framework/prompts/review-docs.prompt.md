---
description: 'Summarize documentation linked from a ticket and surface what is relevant to your work before you start coding.'
agent: 'agent'
tools:
  - 'fetch'
  - 'codebase'
---

# Review Docs

Summarize the documentation linked from your ticket and extract what matters for your implementation.

## Instructions

1. **Read the provided documentation.** If the user has pasted content, summarize it. If URLs are provided, fetch and read them.

2. **Identify what is relevant to the ticket.** Focus on:
   - API contracts, request/response shapes, and field definitions
   - Constraints, validation rules, or known edge cases
   - Prior decisions (ADRs, design notes) that affect your approach

3. **Find the related code.** Search the codebase for existing implementations that interact with the documented system — services, models, API clients, or tests that reference the same endpoints or data structures.

4. **Flag gaps.** If the documentation is incomplete, contradicts the ticket, or leaves decisions unresolved, call them out explicitly.

5. **Ask for help.** If it appears there's a gap in the documentation that prevents you from moving forward, ask the user if there is more context or documentation for you to consume.

## Output Format

```markdown
## Docs Summary: [document or system name]

### What's Relevant to This Ticket
[2–4 bullet points on the parts that directly affect your implementation]

### Key Constraints or Rules
[Validation rules, field requirements, auth requirements, limits, etc.]

### Related Code in This Repo
- [file or module] — [why it's relevant]

### Gaps or Open Questions
- [Anything unclear, missing, or in conflict with the ticket]
```

## Input

Ticket: ${input:ticket:Describe what you are implementing}

Documentation: ${input:docs:Paste the documentation content or provide URLs}
