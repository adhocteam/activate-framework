---
description: 'Generate a QASP alignment report showing how current practices map to quality assurance surveillance plan requirements.'
agent: 'agent'
tools:
  - 'codebase'
---

# QASP Alignment Report

Generate a report that maps the current repository's practices and tooling to common Quality Assurance Surveillance Plan (QASP) requirements found in government software development contracts.

## Report Structure

### 1. Repository Assessment

Scan the repository for evidence of the following practices:

| Practice | What to Look For |
|----------|-----------------|
| **Code review process** | PR templates, review instructions, branch protection evidence |
| **Testing strategy** | Test files, test configuration, coverage settings |
| **Documentation** | ADRs, README quality, inline documentation, session logs |
| **Commit conventions** | Conventional commits, atomic commit patterns |
| **Security practices** | Security instructions, dependency scanning config, secrets management |
| **Accessibility** | A11y tests, accessibility instructions or checks |
| **CI/CD** | Workflow files, deployment configuration |

### 2. QASP Metric Mapping

For each common QASP metric, assess alignment:

| QASP Metric | Current Evidence | Gap Assessment | Recommendation |
|-------------|-----------------|----------------|----------------|
| Code Quality / Technical Debt | | | |
| Sprint Velocity & Predictability | | | |
| Deployment Frequency | | | |
| Change Failure Rate | | | |
| Documentation Currency | | | |
| Accessibility Compliance | | | |

### 3. Activate Practices in Use

Identify which Activate Copilot practices are installed and active:

- [ ] `AGENTS.md` — Project-wide guidance
- [ ] Instruction files — Context-specific rules
- [ ] Skills — Procedural workflows
- [ ] Agent definitions — Specialized personas
- [ ] Session logging — Work traceability
- [ ] Conventional commits — Change tracking

### 4. Recommendations

Provide prioritized recommendations:

1. **Quick wins** — Low effort, high QASP impact
2. **Strategic improvements** — Higher effort, significant quality gains
3. **Future considerations** — Long-term maturity improvements

## Output

Present the report in Markdown format suitable for inclusion in project documentation or stakeholder communication. Use concrete evidence from the repository — link to specific files and configurations rather than making general claims.
