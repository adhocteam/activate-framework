# Activate Copilot

Agent, command, and skill definitions for Ad Hoc's Activate delivery methodology.

## Overview

This repository contains the AI agent configurations, reusable commands, and skill definitions that power Activate's human-led, AI-accelerated delivery approach. These components integrate with GitHub Copilot and other AI tools to augment cross-functional teams while preserving human accountability.

## What is Activate?

Activate is Ad Hoc's approach for building, operating, and improving digital systems. It delivers high-quality speed to value by aligning teams, delivery processes, and technology directly to mission outcomes through a continuous **Learn / Build / Measure** loop.

```mermaid
graph LR
    L[Learn] --> B[Build]
    B --> M[Measure]
    M --> L
    
    style L fill:#347d39,stroke:#46954a,color:#fff
    style B fill:#1f6feb,stroke:#388bfd,color:#fff
    style M fill:#8957e5,stroke:#a371f7,color:#fff
```

- **Learn:** Research and discovery agents synthesize inputs, analyze constraints, and prototype solutions
- **Build:** Spec, design, and code agents translate approved intent into working software through TDD
- **Measure:** Operations and outcome agents analyze data, drafting insights back into backlogs and PRs

## Repository Structure

This repository has two sets of files:

- **Root-level** (`.github/`, `docs/`) — Development-time files for contributors to THIS repo
- **`/src`** — Distributable files that teams receive when installing the starter kit

See [docs/README.md](./docs/README.md) for audience-specific documentation navigation.

```text
activate-copilot/
├── .github/                    # Dev-time guidance (for this repo)
│   ├── instructions/           # Instruction files (Tier 2)
│   ├── skills/                 # Skill definition files (Tier 3)
│   └── agents/                 # Agent definitions (Tier 4)
├── src/                        # Distributable starter kit
│   ├── AGENTS.md               # Template AGENTS.md for teams
│   └── .github/
│       ├── instructions/       # Template instruction files
│       ├── prompts/            # Template prompt files
│       ├── skills/             # Template skill files
│       └── agents/             # Template agent definitions
└── docs/
    ├── user/                   # End-user documentation
    └── dev/                    # Contributor/internal documentation
```

## File Hierarchy

This repository defines a four-tier hierarchy for AI agent guidance (see [ADR-001](./docs/dev/adrs/ADR-001-agent-instructions-skills-files.md)):

| Tier | Type | Location | Scope | Invocation |
|------|------|----------|-------|------------|
| 1 | AGENTS.md | Repository root | Project-wide | Always active |
| 2 | Instruction files | `.github/instructions/` | Context-specific | Automatic via glob patterns |
| 2 | Prompt files | `.github/prompts/` | Task-specific | On-demand via `/command` |
| 3 | Skills | `.github/skills/[skill-name]/SKILL.md` | Procedural | Explicit, on-demand |
| 4 | Agent definitions | `.github/agents/` | Persona + capabilities | Explicit |

- **AGENTS.md** defines how we work: commit conventions, branching strategy, TDD expectations
- **Instruction files** provide context-specific guidance: language conventions, code review checklists
- **Skills** are reusable procedures: creating an ADR, scaffolding a component
- **Agent definitions** combine persona, capabilities, and which skills/instructions to use

See [EXAMPLE-USAGE.md](./EXAMPLE-USAGE.md) for a walkthrough of how a cross-functional team uses this hierarchy.

## Core Principles

This repository follows key delivery principles:

| Principle | Description |
|-----------|-------------|
| **Human-Led, AI-Assisted** | AI drafts and implements; humans approve and remain accountable |
| **Spec-Driven Execution** | Specifications define problems and acceptance criteria; AI consumes specs to draft code, tests, and docs |
| **Continuous Traceability** | Persistent linkage from outcome → hypothesis → backlog → PR → test → deploy → metric |
| **Test-Driven Development** | Red/green/refactor as non-negotiable guardrails |

## Installation

### Option 1: Installer (Recommended)

The easiest way to get started is using the `/activate` installer skill, which analyzes your repository and installs only what you need:

```text
@workspace /activate install
```

The installer will:

- Detect your languages and frameworks
- Recommend the appropriate bundle (minimal, standard, or full)
- Install only relevant instructions for your stack
- Customize `AGENTS.md` with your project context
- Guide you through the process interactively

**To update later:**

```text
@workspace /activate update
```

### Option 2: Manual Installation

Download `activate-copilot-v*.zip` from the [latest release](https://github.com/adhocteam/activate-copilot/releases/latest).

**Steps:**

1. Download and unzip the bundle
2. Enter the extracted folder and run:

   ```bash
   cd activate-copilot-v*
   node install.mjs
   ```

3. (Optional) Manual mode: copy files from `plugins/activate-framework/` into your repository
4. Customize `AGENTS.md` with your project-specific conventions
5. (Optional) Commit the new files to share with your team:

   ```bash
   git add AGENTS.md .github/
   git commit -m "feat: add Activate Copilot starter kit"
   ```

### What You Get

- **`AGENTS.md`** — Project-wide AI guidance (always active)
- **`.github/instructions/`** — Context-specific rules triggered by file patterns
- **`.github/prompts/`** — Reusable prompt files invoked as `/commands` in chat
- **`.github/skills/`** — Procedural workflows invoked on-demand (Full bundle)
- **`.github/agents/`** — Specialized agent personas (Full bundle)

## Agent Capabilities

Agents in this repository support bounded tasks across the delivery lifecycle:

### Research & Discovery (Learn)

- Research synthesis and thematic analysis
- Constraint awareness and policy checking
- Hypothesis quality improvement

### Spec, Design & Code (Build)

- Spec-driven code generation
- Test generation and updates
- PR creation and iteration
- Design-to-code alignment

### Quality & Risk (Cross-cutting)

- Code quality analysis
- Security and accessibility checks
- Definition of Done enforcement

### Telemetry & Outcomes (Measure)

- Post-release analysis
- Outcome hypothesis validation
- Continuous learning capture

## Getting Started

See [AGENTS.md](./AGENTS.md) for development guidelines, workflow requirements, and contribution standards.

## Activate Core Dispatch Contract

Tasks 1-5 of the cross-org update plan introduce the baseline contract, receiver template, and delivery guardrails:

- Target registry: [`.github/activate-core/targets.yml`](./.github/activate-core/targets.yml)
- Dispatch payload schema: [`.github/activate-core/dispatch-payload.schema.json`](./.github/activate-core/dispatch-payload.schema.json)
- Registry validator: [`scripts/validate-target-registry.mjs`](./scripts/validate-target-registry.mjs)
- Dispatcher workflow: [`.github/workflows/dispatch-activate-core-updates.yml`](./.github/workflows/dispatch-activate-core-updates.yml)
- Dispatcher script: [`scripts/dispatch-core-updates.mjs`](./scripts/dispatch-core-updates.mjs)
- Receiver workflow template: [`templates/activate-core-receiver.workflow.yml`](./templates/activate-core-receiver.workflow.yml)
- Guardrail workflow: [`.github/workflows/validate-activate-core-delivery.yml`](./.github/workflows/validate-activate-core-delivery.yml)
- Guardrail validator: [`scripts/validate-core-delivery.mjs`](./scripts/validate-core-delivery.mjs)

## Related Resources

- [ADR-005: Open-Source Thin Activate Layer](./docs/dev/adrs/ADR-005-open-source-thin-activate-layer.md)
- [ADR-006: Separate Documentation by Audience](./docs/dev/adrs/ADR-006-docs-audience-separation.md)
- [GitHub Copilot Starter Kit Plan](./docs/dev/plans/github-copilot-starter-kit-plan.md)
- [VS Code Customization Docs](https://code.visualstudio.com/docs/copilot/copilot-customization) — How VS Code's built-in customization primitives work
- [VS Code Agent Customization Skill](https://github.com/microsoft/vscode-copilot-chat/tree/main/assets/prompts/skills/agent-customization/) — The built-in skill that understands these file types

## Generator Guidance Overview

This directory holds the authoring-time resources used to build distributable guidance found under `src/`.

### Structure

| Path | Purpose |
|------|---------|
| `instructions/distribution-builder.instructions.md` | Passive guardrails for any `src/**` edits—enforces ADR-001 hierarchy, naming, and template usage |
| `skills/distribution-builder/SKILL.md` | Active workflow for generating all four distributable file types from `templates/` |
| `agents/` | Reserved for specialized personas if the workflow grows more complex |

### How They Work Together

- **Skill (explicit):** Invoke `distribution-builder` to scaffold new files in `src/` using the placeholder templates.
- **Instruction (implicit):** Activates automatically whenever you edit files under `src/`, providing guardrails without explicit invocation.

Per [ADR-001](docs/dev/adrs/ADR-001-agent-instructions-skills-files.md), the skill consumes templates in `templates/` and emits AGENTS.md, instruction, skill, and agent files. The instruction ensures subsequent edits stay compliant.
