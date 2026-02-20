---
description: 'Universal coding conventions and workflow expectations'
applyTo: '**'
excludeAgent: []
---
# General Instructions

Baseline conventions for all code contributions. Teams should customize these to match their project's technology stack, tooling, and team preferences.

## When To Use

- Starting any new feature, fix, or refactor
- Writing or reviewing code in any language
- Creating or updating documentation
- Working with AI coding assistants

## Code Conventions

### Naming

<!-- CUSTOMIZE: Update naming conventions to match your primary language and team style guide -->

- Use descriptive, intention-revealing names for variables, functions, and classes
- Follow language-specific conventions (e.g., `snake_case` for Python, `camelCase` for JavaScript)
- Prefer clarity over brevity; avoid single-letter names except in tight loops
- Name booleans as questions (e.g., `is_valid`, `hasPermission`, `shouldRetry`)

### Structure

- Keep functions and methods focused on a single responsibility
- Limit function length; extract helpers when logic becomes complex
- Organize imports consistently (standard library, third-party, local)
- Group related code together; separate concerns into modules

### Comments and Documentation

- Write code that explains itself; use comments for "why", not "what"
- Document public APIs with clear descriptions of purpose, parameters, and return values
- Keep comments up to date when code changes
- Include usage examples in documentation where helpful

## Git Workflow

### Commits

<!-- CUSTOMIZE: Add or modify commit types to match your team's conventions -->

- Write atomic commits that represent a single logical change
- Use conventional commit messages: `type: description`
- Types: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`
- Keep the subject line under 72 characters; add detail in the body if needed

### Branches

<!-- CUSTOMIZE: Adjust branch naming pattern and base branch if different (e.g., develop, trunk) -->

- Create feature branches from the main branch
- Use descriptive branch names (e.g., `feat/user-authentication`, `fix/login-redirect`)
- Keep branches short-lived; merge back frequently
- Delete branches after merging

### Pull Requests

<!-- CUSTOMIZE: Adjust PR size limit and required reviewers based on team policy -->

- Link PRs to related issues
- Provide context in the PR description: what, why, and how to test
- Keep PRs focused and reviewable (aim for under 400 lines changed)
- Respond to review feedback promptly

## Working with AI Assistants

### Effective Prompting

- Provide context: what you're trying to accomplish and relevant constraints
- Be specific about the desired output format or approach
- Reference existing patterns in the codebase when applicable
- Break complex requests into smaller, focused asks

### Review AI-Generated Code

- Verify logic correctness; don't assume AI output is bug-free
- Check for security issues, especially with user input and external calls
- Ensure generated code follows project conventions
- Test thoroughly before committing

### Collaboration Boundaries

- AI assists; humans decide and remain accountable
- Review all AI-generated changes before committing
- Use AI suggestions as starting points, not final answers
- Escalate to teammates when uncertain

## Quality Expectations

### Before Submitting Code

<!-- CUSTOMIZE: Add project-specific commands (e.g., npm test, pytest, make lint) -->

- Run tests locally and ensure they pass
- Run linters and formatters per project configuration
- Self-review your diff for obvious issues
- Verify the change works as intended

### Definition of Done

<!-- CUSTOMIZE: Add project-specific criteria (e.g., accessibility checks, security scan, design review) -->

- Code compiles/runs without errors
- Tests cover new functionality and edge cases
- Documentation updated if behavior changed
- No unresolved TODO comments without linked issues

## Customization Notes

<!-- Teams should update this section with project-specific details -->

- **Language/Framework**: <!-- e.g., Python 3.12 / FastAPI, TypeScript / Next.js -->
- **Formatting**: <!-- e.g., Black, Prettier, rustfmt -->
- **Linting**: <!-- e.g., Ruff, ESLint, Clippy -->
- **Test Framework**: <!-- e.g., pytest, Jest, Vitest -->
- **CI Pipeline**: <!-- e.g., GitHub Actions, CircleCI -->
