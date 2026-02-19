# Creating New Customization Files

This project uses VS Code's [agent customization](https://code.visualstudio.com/docs/copilot/copilot-customization) primitives to provide AI-assisted development guidance. When you need to create a new instruction file, skill, prompt, or agent definition, VS Code can help.

## Use VS Code's Built-in Skill

VS Code includes a built-in **agent-customization** skill that understands the full set of customization primitives. When you ask Copilot to create a new customization file, this skill automatically:

1. **Selects the appropriate primitive** based on your intent
2. **Places the file** in the correct directory
3. **Generates valid frontmatter** with required fields
4. **Validates** the result

You do not need to memorize file formats or directory conventions — the built-in skill handles this for you.

## How to Create a New File

In VS Code's Copilot chat, describe what you need. For example:

- *"Create an instruction file for Python code style in this project"*
- *"Add a prompt for generating unit tests"*
- *"Set up a skill for database migration workflows"*
- *"Create an agent that specializes in security reviews"*

The agent-customization skill will determine the right primitive and walk you through creating it.

## Work Iteratively from Your Code

The most effective way to create customization files is to let Copilot derive them from your actual codebase. Rather than writing guidance from scratch, point the agent at your existing code and let it identify patterns worth codifying.

### Start from what's already there

Open your project in VS Code and ask Copilot to analyze your code for conventions. For example:

- *"Look through the code in this repo and identify common patterns, naming conventions, and style choices that we should document as instruction files"*
- *"Review our API routes and suggest an instruction file that captures our error handling conventions"*
- *"Examine our React components and create an instruction file for the component patterns we follow"*

### Refine through conversation

The first draft is a starting point. Work back and forth with Copilot to refine the output:

1. **Generate** — Ask the agent to analyze your code and draft a customization file
2. **Review** — Read through what it produced and note what's missing or over-specified
3. **Refine** — Ask it to adjust: *"Add our logging conventions"* or *"Remove the section about testing — we'll handle that separately"*
4. **Validate** — Try using the new file in a real task to see if it produces the behavior you want

### Build up over time

You don't need to capture everything at once. Start with the conventions that matter most — the ones new team members get wrong or that cause the most code review friction — and add more files as patterns emerge.

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

## Further Reading

- [VS Code Copilot Customization docs](https://code.visualstudio.com/docs/copilot/copilot-customization)
