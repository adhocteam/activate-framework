---
description: 'Universal code review checklist for all project types'
applyTo: '**'
excludeAgent: ["coding-agent"]
---
# Code Review Instructions

Guidelines for authors submitting code and reviewers evaluating it.

**Important**: When reviewing code in specific languages or technologies, refer to the corresponding instruction files in `.github/instructions/*.instructions.md` for language-specific best practices, conventions, and review criteria.

## Reviewer Role & Tone

- Write as a **collaborative peer**, not a gatekeeper
- Aim to **explain** rather than simply critique—highlight positive intent where relevant
- Keep tone **professional**, **constructive**, and **concise**
- Focus on the code, not the person

## Review Priorities

When performing a code review, prioritize issues in the following order:

### 🔴 CRITICAL (Block merge)

- Security vulnerabilities, exposed secrets, authentication issues
- Logic errors, data corruption risks, race conditions
- Command injection or shell escape issues

### 🟡 IMPORTANT (Requires discussion)

- Code quality violations (SOLID principles, excessive duplication)
- Missing tests for critical paths
- Performance bottlenecks (N+1 queries, memory leaks)

### 🟢 SUGGESTION (Non-blocking)

- Readability improvements, naming, simplification
- Minor best practice deviations
- Documentation gaps

## Code Review Principles

- **Be specific**: Provide exact file paths, line numbers, and clear issue descriptions
- **Be concise and direct**: Use short, imperative statements rather than long paragraphs
- **Focus on actionable feedback**: Avoid vague directives like "be more accurate" or "identify all issues"
- **Explain why**: Share your reasoning and link to documentation when possible
- **Group related comments**: Avoid multiple comments about the same topic
- **Structure matters**: Use bullet points and clear headings for organization
- **Show examples**: Demonstrate concepts with sample code when clarification is needed
- **Balance feedback**: Tell authors what to keep, not just what to change
- **Be curious**: Ask questions to check assumptions and understand intent
- **Avoid generic praise**: Remove purely complimentary comments; focus on improvements needed

### Anti-Patterns to Avoid

- **Nitpicking**: Weigh importance against time/effort required
- **Law of triviality**: Avoid spending large amounts of time and energy on trivial topics
- **Style debates**: Move stylistic concerns to separate meetings or RFCs; automate with linters

## Before Starting a Review

1. Use the active pull request context to understand the PR background
2. Review the project's contributing guidelines if available
3. Check for related GitHub issues referenced in the PR description
4. Look at any previous discussions and comments on the PR

### Handling Review Limitations

- If files are too large to analyze completely, focus on critical changes and note the limitation
- If unable to access certain files, note this in the review
- When context is unclear, ask clarifying questions rather than making assumptions

## Comment Format

Structure review comments consistently:

```markdown
**[PRIORITY] Category: Brief title**

Description of the issue.

**Why this matters:** Impact explanation.

**Suggested fix:** [code example if applicable]
```

Example:

```markdown
**[CRITICAL] Security: SQL injection vulnerability**

User input is passed directly to the query without sanitization.

**Why this matters:** Attackers could extract or modify database contents.

**Suggested fix:**
Use parameterized queries instead of string concatenation.
```

## Good vs. Concerning Patterns

| Good Practice | Why It Matters |
|---------------|----------------|
| Clear function and variable names | Improves long-term maintainability |
| Avoiding deeply nested logic | Enhances legibility and testability |
| Early returns for edge cases | Reduces cognitive complexity |
| Descriptive commit messages | Helps future maintainers understand intent |

| Concerning Pattern | Why It's Problematic |
|--------------------|----------------------|
| Silent failure or catch-all `try/catch` | Masks real errors and makes debugging harder |
| Hard-coded credentials or secrets | Poses a security risk |
| Redundant code paths | Increases complexity without added value |
| Magic numbers without constants | Reduces code clarity and maintainability |

## Approval Readiness Checklist

Before approving, verify:

- [ ] Code changes include appropriate test coverage
- [ ] No regressions or backward-incompatible changes unless justified
- [ ] Code style and project conventions are followed
- [ ] Adequate inline documentation or comments are present
- [ ] Edge cases and error handling are covered
- [ ] No security vulnerabilities introduced
- [ ] Performance implications have been considered
