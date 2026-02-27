# Activate Framework

Baseline AI agent guidance for cross-functional government delivery teams, distributed from the [Activate Copilot](https://github.com/adhocteam/activate-copilot) starter kit.

## Overview

This repository receives the core Activate framework — instruction files, prompt files, and project-wide guidance — via an automated cross-org delivery pipeline. These files integrate with GitHub Copilot and VS Code to provide consistent, human-led AI-assisted development practices.

## What is Activate?

Activate is Ad Hoc's approach for building, operating, and improving digital systems. It delivers high-quality speed to value by aligning teams, delivery processes, and technology directly to mission outcomes through a continuous **Learn / Build / Measure** loop.

- **Learn:** Research and discovery — synthesize inputs, analyze constraints, prototype solutions
- **Build:** Spec, design, and code — translate approved intent into working software through TDD
- **Measure:** Operations and outcomes — analyze data, draft insights back into backlogs and PRs

## Repository Structure

```text
activate-framework/
├── .github/
│   └── workflows/
│       └── activate-core-receiver.workflow.yml  # Automated update receiver
├── activate-framework/                          # Distributed framework files
│   ├── AGENTS.md                                # Project-wide AI guidance
│   ├── CUSTOMIZATION.md                         # Customization guide
│   ├── instructions/                            # Context-specific rules
│   │   ├── general.instructions.md
│   │   └── security.instructions.md
│   └── prompts/                                 # Reusable prompt files
│       ├── accessibility-check.prompt.md
│       ├── code-review.prompt.md
│       └── create-adr.prompt.md
├── docs/                                        # Documentation
│   ├── README.md
│   └── user/
│       └── adoption-guide.md
├── AGENTS.md                                    # Repo-level working guidelines
└── README.md                                    # This file
```

## Distributed Files

| File | Purpose |
|------|---------|
| `AGENTS.md` | Project-wide AI guidance — commit conventions, TDD expectations, workflow requirements |
| `CUSTOMIZATION.md` | Guide for tailoring the framework to your team's needs |
| `instructions/general.instructions.md` | General development guidance |
| `instructions/security.instructions.md` | Security-focused review rules |
| `prompts/accessibility-check.prompt.md` | Accessibility compliance check |
| `prompts/code-review.prompt.md` | Code review workflow |
| `prompts/create-adr.prompt.md` | Architecture Decision Record scaffolding |

## Getting Started

1. Review the files in `activate-framework/` to understand the guidance provided
2. See [CUSTOMIZATION.md](./activate-framework/CUSTOMIZATION.md) for how to adapt the framework to your project
3. See [docs/user/adoption-guide.md](./docs/user/adoption-guide.md) for a guide to introducing Activate practices on your team
4. See [AGENTS.md](./AGENTS.md) for this repo's working guidelines

## Related Resources

- [Activate Copilot](https://github.com/adhocteam/activate-copilot) — Upstream source repository
- [VS Code Customization Docs](https://code.visualstudio.com/docs/copilot/copilot-customization) — How VS Code's built-in customization primitives work
