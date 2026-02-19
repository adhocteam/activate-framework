# Activate Framework

A starter kit for AI-assisted development workflows, built for teams delivering digital services in government and public-sector environments.

## Overview

Activate is an approach for building, operating, and improving digital systems. It delivers high-quality speed to value by aligning teams, delivery processes, and technology directly to mission outcomes through a continuous **Learn / Build / Measure** loop.

```mermaid
graph LR
    L[Learn] --> B[Build]
    B --> M[Measure]
    M --> L
    
    style L fill:#347d39,stroke:#46954a,color:#fff
    style B fill:#1f6feb,stroke:#388bfd,color:#fff
    style M fill:#8957e5,stroke:#a371f7,color:#fff
```

This repository provides a curated set of guidance files — instructions, prompts, and an AGENTS.md baseline — that integrate with GitHub Copilot and other AI tools to augment cross-functional teams while preserving human accountability.

## Repository Structure

```text
activate-framework/
├── AGENTS.md                                    # Project-wide AI guidance (always active)
├── CUSTOMIZATION.md                             # Guide for creating new customization files
├── instructions/
│   ├── general.instructions.md                  # General development conventions
│   └── security.instructions.md                 # Security-focused guidance
└── prompts/
    ├── accessibility-check.prompt.md            # /accessibility-check command
    ├── code-review.prompt.md                    # /code-review command
    └── create-adr.prompt.md                     # /create-adr command
docs/
└── user/
    └── adoption-guide.md                        # Rollout guidance for teams and agencies
```

## File Hierarchy

This framework uses a tiered hierarchy for AI agent guidance:

| Tier | Type | Location | Scope | Invocation |
|------|------|----------|-------|------------|
| 1 | AGENTS.md | Repository root | Project-wide | Always active |
| 2 | Instruction files | `.github/instructions/` | Context-specific | Automatic via glob patterns |
| 2 | Prompt files | `.github/prompts/` | Task-specific | On-demand via `/command` |
| 3 | Skills | `.github/skills/[skill-name]/SKILL.md` | Procedural | Explicit, on-demand |
| 4 | Agent definitions | `.github/agents/` | Persona + capabilities | Explicit |

- **AGENTS.md** defines how we work: commit conventions, branching strategy, TDD expectations
- **Instruction files** provide context-specific guidance: language conventions, code review checklists
- **Prompt files** are reusable tasks invoked as `/commands`: code reviews, accessibility checks, ADR scaffolding
- **Skills** are reusable procedures: creating an ADR, scaffolding a component
- **Agent definitions** combine persona, capabilities, and which skills/instructions to use

> This repository includes Tiers 1 and 2. Teams can extend with their own skills (Tier 3) and agent definitions (Tier 4) as needed. See [CUSTOMIZATION.md](./activate-framework/CUSTOMIZATION.md) for guidance.

## Installation

Copy the contents of the `activate-framework/` directory into your repository:

```bash
# From this repo's root
cp -r activate-framework/* /path/to/your-repo/
```

Then place the files in the standard VS Code customization locations:

```bash
# In your target repository
cp AGENTS.md .
cp CUSTOMIZATION.md .
mkdir -p .github/instructions .github/prompts
cp instructions/* .github/instructions/
cp prompts/* .github/prompts/
```

After installation:

1. Review and customize `AGENTS.md` with your project-specific conventions
2. Review the instruction files and adjust for your tech stack
3. Commit the new files:

   ```bash
   git add AGENTS.md CUSTOMIZATION.md .github/
   git commit -m "feat: add Activate framework guidance files"
   ```

### What You Get

- **`AGENTS.md`** — Project-wide AI guidance (always active)
- **`CUSTOMIZATION.md`** — How to create new instruction files, prompts, skills, and agents
- **`.github/instructions/`** — Context-specific rules triggered by file patterns
- **`.github/prompts/`** — Reusable prompt files invoked as `/commands` in chat

## Core Principles

| Principle | Description |
|-----------|-------------|
| **Human-Led, AI-Assisted** | AI drafts and implements; humans approve and remain accountable |
| **Spec-Driven Execution** | Specifications define problems and acceptance criteria; AI consumes specs to draft code, tests, and docs |
| **Continuous Traceability** | Persistent linkage from outcome → hypothesis → backlog → PR → test → deploy → metric |
| **Test-Driven Development** | Red/green/refactor as non-negotiable guardrails |

## Adoption Guide

For guidance on rolling out Activate across teams, see the [Adoption Guide](./docs/user/adoption-guide.md). It covers:

- Which context type to use and when
- Rollout patterns for single-team, multi-team, and enterprise scenarios
- Forking vs. referencing strategies
- How to keep up with upstream updates

## Updates

This repository receives periodic updates from the upstream Activate project. Updates are delivered automatically via a receiver workflow and opened as pull requests for review.

## Related Resources

- [VS Code Customization Docs](https://code.visualstudio.com/docs/copilot/copilot-customization) — How VS Code's built-in customization primitives work
- [VS Code Agent Customization Skill](https://github.com/microsoft/vscode-copilot-chat/tree/main/assets/prompts/skills/agent-customization/) — The built-in skill that understands these file types

## Related Work

- [cloud-gov-instructions](https://github.com/adhocteam/cloud-gov-instructions) — AI-assisted development guidance tailored for teams building on cloud.gov, also maintained by Ad Hoc

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines on how to participate.

## License

This project is licensed under the MIT License. See [LICENSE](./LICENSE) for details.