# Creating New Customization Files

This project uses VS Code's [agent customization](https://code.visualstudio.com/docs/copilot/copilot-customization) primitives to provide AI-assisted development guidance. When you need to create a new instruction file, skill, prompt, or agent definition, VS Code can help.

## Use VS Code's Built-in Skill

VS Code includes a built-in **agent-customization** skill that understands the full set of customization primitives. When you ask Copilot to create a new customization file, this skill automatically:

1. **Selects the appropriate primitive** based on your intent
2. **Places the file** in the correct directory
3. **Generates valid frontmatter** with required fields
4. **Validates** the result

You do not need to memorize file formats or directory conventions — the built-in skill handles this for you.

## What Makes Customization Files Effective

- **Expert-curated skills deliver measurable improvement.** Curated skills raise agent task pass rates (according to some studies) by an average of 16 percentage points, with gains varying widely by domain.
- **AI self-generated skills provide no benefit on average.** Models cannot reliably author the procedural knowledge they benefit from consuming. Letting an agent write its own skills by itself without expert review may produce negligible or even negative effects.
- **Focused skills outperform comprehensive documentation.** Skills scoped to 2–3 modules consistently outperform broad, all-encompassing guidance files.
- **Skills are a force multiplier.** Smaller models equipped with well-crafted skills can match the performance of larger models operating without them.

### What this means in practice

1. **Human expertise is the essential ingredient.** Use AI to draft customization files, but treat every output as a starting point that requires expert review and curation — not a finished product.
2. **Keep skills focused.** A skill that does one workflow well is more valuable than a comprehensive reference document. Aim for 2–3 tightly scoped procedural modules per skill.
3. **Not every task benefits from a skill.** Some tasks show negative effects when skills are applied. Validate that a new skill actually improves outcomes before distributing it.
4. **Invest curation effort where it matters most.** Gains vary by domain. Prioritize creating skills for areas where your team encounters the most friction or inconsistency.

## How to Create a New File

In VS Code's Copilot chat, describe what you need. For example:

- *"Create an instruction file for Python code style in this project"*
- *"Add a prompt for generating unit tests"*
- *"Set up a skill for database migration workflows"*
- *"Create an agent that specializes in security reviews"*

The agent-customization skill will determine the right primitive and walk you through creating it.

## Work Iteratively from Your Code

The most effective way to create customization files is to combine AI-assisted drafting with expert curation. Point the agent at your existing code to identify patterns, then apply your team's judgment to shape the output into focused, reliable guidance.

> **Key principle:** AI is good at identifying patterns in your code, but some research shows that AI-generated skills used without expert review produce no measurable benefit. Your team's knowledge is what turns a draft into an effective skill.

### Start from what's already there

Open your project in VS Code and ask Copilot to analyze your code for conventions. For example:

- *"Look through the code in this repo and identify common patterns, naming conventions, and style choices that we should document as instruction files"*
- *"Review our API routes and suggest an instruction file that captures our error handling conventions"*
- *"Examine our React components and create an instruction file for the component patterns we follow"*

### Curate with expert judgment

The first draft is a starting point — not a finished product. Work back and forth with Copilot, but apply your domain expertise at each step:

1. **Generate** — Ask the agent to analyze your code and draft a customization file
2. **Review critically** — Read through what it produced. Is every rule accurate? Remove anything speculative or overly broad. AI-generated guidance that is wrong or vague will degrade performance, not improve it.
3. **Focus the scope** — Keep each file tightly scoped. If a draft covers too many concerns, split it. Focused skills (2–3 modules) consistently outperform comprehensive documents.
4. **Refine** — Ask the agent to adjust: *"Add our logging conventions"* or *"Remove the section about testing — we'll handle that separately"*
5. **Validate** — Try using the new file in a real task to see if it produces the behavior you want. If it doesn't improve outcomes, revise or remove it.

### Build up over time

You don't need to capture everything at once. Start with the conventions that matter most — the ones new team members get wrong or that cause the most code review friction — and add more files as patterns emerge.

### Avoid common pitfalls

- **Don't accept AI-generated files as-is.** Always apply expert review. Uncurated AI output has been shown to provide no measurable benefit.
- **Don't create skills for everything.** Some tasks don't benefit from additional guidance. Over-specifying can confuse agents and reduce quality.
- **Don't make skills too broad.** A single file trying to cover an entire domain is less effective than several focused files.

## Customization Primitives

For reference, here are the available file types and where they live:

| Primitive | File Pattern | Location | When to Use |
|-----------|-------------|----------|-------------|
| Workspace Instructions | `AGENTS.md` | Repository root | Always-on guidance for the whole project |
| File Instructions | `*.instructions.md` | `.github/instructions/` | Context-specific rules via `applyTo` patterns |
| Prompts | `*.prompt.md` | `.github/prompts/` | Single focused task, invoked with `/command` |
| Skills | `SKILL.md` | `.github/skills/<name>/` | Multi-step workflow with bundled assets |
| Custom Agents | `*.agent.md` | `.github/agents/` | Specialized persona with tool restrictions |

## Quick Decision Guide

- **Applies to most work in the project?** → Workspace Instructions (`AGENTS.md`)
- **Applies to specific file types or contexts?** → File Instructions (`.instructions.md`)
- **A repeatable single task?** → Prompt (`.prompt.md`)
- **A multi-step workflow with scripts or templates?** → Skill (`SKILL.md`)
- **Needs its own persona, tools, or context isolation?** → Custom Agent (`.agent.md`)

## Model Selection

In addition to customizing agent behavior with instructions, prompts, skills, and agents, you can control which AI model handles different tasks. Key options:

- **Model picker** — Manually select a model per conversation in the chat input field
- **Auto model selection** — Let VS Code route requests to the optimal model based on task complexity
- **Per-agent model pinning** — Add `model: Model Name (vendor)` to a custom agent's frontmatter to always use a specific model for that agent
- **Utility model settings** — Configure `chat.utilityModel` and `chat.utilitySmallModel` to use faster/cheaper models for background tasks (commit messages, titles, etc.)
- **Bring Your Own Key (BYOK)** — Connect models from Azure, Anthropic, Gemini, OpenAI, local providers, or any custom endpoint

For a comprehensive guide to all model management options, see [VS Code Language Models documentation](https://code.visualstudio.com/docs/agent-customization/language-models).

## Further Reading

- [VS Code Copilot Customization docs](https://code.visualstudio.com/docs/copilot/copilot-customization)
- [AI Language Models in VS Code](https://code.visualstudio.com/docs/agent-customization/language-models)
