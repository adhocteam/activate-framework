---
description: 'Reproduce a bug in your local environment before fixing it, confirming the failure and documenting a clear repro case.'
agent: 'agent'
tools:
  - 'codebase'
---

# Reproduce Bug

Walk through reproducing the bug described in this ticket. Confirm the failure exists in your environment before writing any fix.

## Instructions

1. **Read the repro steps** from the ticket. If none are provided, ask the user to describe the failure before proceeding.

2. **How long has the bug existed?** Read the ticket for any clues on when the bug was introduced. This can help you narrow down where to look in the codebase and which commits to review. If the ticket doesn't say, ask the user if they have any idea when it started happening or if it's a new issue. This isn't critical to find out, but can be helpful if we know.

3. **Identify the affected code.** Search the codebase for the files, functions, or routes most likely involved in the failure.

4. **Check recent changes.** Look at recent commits touching the affected area — the bug may already be fixed, or a recent change may have introduced it.

5. **Guide the developer through reproduction.** Based on the ticket and codebase, describe:
   - The exact setup required (test data, feature flags, user state, environment)
   - The specific steps to trigger the failure
   - What the broken behavior looks like
   - What the correct behavior should be

6. **Document the repro case** in the format below. This becomes the basis for a regression test.

7. **Ask a human for help.** If the repro steps in the ticket are unclear and you're not confident about how to reproduce the bug, tell the user to ask for help from a teammate who might have more context.

## Output Format

```markdown
## Bug Repro: [ticket title or short description]

### Environment
- [Any relevant environment details: browser, OS, feature flags, user role, etc.]

### Steps to Reproduce
1. [Step 1]
2. [Step 2]
3. ...

### Actual Behavior
[What currently happens]

### Expected Behavior
[What should happen instead]

### Affected Code
- [file path or function name]

### Notes
[Any assumptions, related commits, or edge cases observed]
```

## Input

Ticket: ${input:ticket:Paste the bug ticket description or provide a summary of the failure}
