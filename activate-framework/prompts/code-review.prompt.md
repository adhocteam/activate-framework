---
description: 'Run a structured code review on the current file or selection using the project code review checklist.'
agent: 'agent'
tools:
  - 'changes'
---

# Code Review

Perform a structured code review on the provided code. Follow the priority-based review approach below.

## Review Priorities

Evaluate issues in this order:

### Critical (Block merge)

- Security vulnerabilities, exposed secrets, authentication issues
- Logic errors, data corruption risks, race conditions
- Command injection or shell escape issues

### Important (Requires discussion)

- Code quality violations (SOLID principles, excessive duplication)
- Missing tests for critical paths
- Performance bottlenecks (N+1 queries, memory leaks)

### Suggestion (Non-blocking)

- Readability improvements, naming, simplification
- Minor best practice deviations
- Documentation gaps

## Review Instructions

1. Read the code carefully and identify the purpose of each change.
2. Check for issues in priority order (Critical → Important → Suggestion).
3. For each finding, include:
   - **Priority level** and **category**
   - **File and location** of the issue
   - **Why it matters** — explain the impact
   - **Suggested fix** — provide a code example when applicable
4. Note positive patterns worth keeping.
5. Summarize with a clear recommendation: approve, request changes, or needs discussion.

## Context

If a `code-review.instructions.md` file exists in `.github/instructions/`, follow any project-specific review criteria defined there in addition to the priorities above.

Review: ${selection}
