---
name: activate-installer
description: Installs Activate Copilot in a repository with intelligent customization. Use when asked to install, set up, or update Activate.
inputs:
  - name: bundle
    description: 'minimal, standard, or full. Defaults to standard.'
    required: false
outputs:
  - name: installed_version
    description: The version of Activate Copilot installed
  - name: installed_files
    description: List of files created or updated
---

# Activate Installer Skill

## Purpose

Installs Activate Copilot with intelligent customization based on repository analysis. Makes the installation experience **self-demonstrating**—users experience AI assistance immediately by watching the skill work.

## When to Invoke

- User asks to "install Activate" or "set up Activate Copilot"
- User asks to "update Activate" or "check for updates"
- New repository needs Activate configuration

## Preconditions

- Repository is initialized (has `.git/`)
- User has write access
- GitHub CLI (`gh`) available (or manual download)

## Workflow

### Step 1: Analyze Repository

Detect languages, frameworks, and tools to customize the installation.

**Check for languages:**

```bash
# Python
ls pyproject.toml requirements.txt setup.py 2>/dev/null

# TypeScript/JavaScript
ls package.json tsconfig.json 2>/dev/null

# Ruby
ls Gemfile 2>/dev/null

# Go
ls go.mod 2>/dev/null
```

**Check for frameworks:**

```bash
# Python frameworks
grep -l "fastapi\|flask\|django" **/*.py 2>/dev/null | head -1

# JS frameworks
grep "\"next\"\|\"react\"\|\"vue\"" package.json 2>/dev/null
```

**Present findings:**

```text
📊 Repository Analysis:

Languages:
  ✓ Python 3.11 (pyproject.toml)
  ✓ TypeScript (package.json)

Frameworks:
  ✓ FastAPI (detected in src/)
  ✓ React (package.json)

Recommended bundle: standard
```

### Step 2: Select Bundle

Recommend bundle based on analysis:

- **minimal**: Single language, simple project → security + general instructions
- **standard**: Multiple languages → adds code review + language-specific instructions
- **full**: Complex workflows → adds skills and agents

Confirm with user:

```text
I recommend the 'standard' bundle which includes:
- AGENTS.md (workflow guidance)
- Security and general instructions
- Python and TypeScript instructions
- Code review checklist

Which bundle would you like?
```

### Step 3: Download Bundle

**Using GitHub CLI:**

```bash
gh release download \
  --repo adhocteam/activate-copilot \
  --pattern "activate-standard-*.zip" \
  --clobber
```

**Or provide manual link:**

```text
Download from: https://github.com/adhocteam/activate-copilot/releases/latest
```

### Step 4: Extract and Review

```bash
# Extract to temp location
TEMP_DIR=$(mktemp -d)
unzip -q activate-standard-*.zip -d "$TEMP_DIR"

# Show what will be installed
ls -la "$TEMP_DIR"
```

Show user the file list:

```text
Files to be installed:

✓ AGENTS.md
✓ .github/instructions/security.instructions.md
✓ .github/instructions/general.instructions.md
✓ .github/instructions/python.instructions.md
✓ .github/instructions/typescript.instructions.md
✓ .github/instructions/code-review.instructions.md
✓ .github/.activate-version
```

### Step 5: Install Files

**Handle existing AGENTS.md:**

If AGENTS.md exists, backup first:

```bash
mv AGENTS.md AGENTS.md.backup-$(date +%Y%m%d)
```

**Install selectively based on analysis:**

```bash
# Always install core files
cp "$TEMP_DIR/AGENTS.md" AGENTS.md
cp "$TEMP_DIR/.github/instructions/security.instructions.md" .github/instructions/
cp "$TEMP_DIR/.github/instructions/general.instructions.md" .github/instructions/
cp "$TEMP_DIR/.github/instructions/code-review.instructions.md" .github/instructions/

# Install language-specific files if detected
if [[ -f pyproject.toml ]]; then
    cp "$TEMP_DIR/.github/instructions/python.instructions.md" .github/instructions/
fi

if [[ -f package.json ]]; then
    cp "$TEMP_DIR/.github/instructions/typescript.instructions.md" .github/instructions/
fi

# Write version marker
echo "v1.5.0" > .github/.activate-version
```

### Step 6: Customize AGENTS.md

Add project-specific context discovered in Step 1:

```markdown
## Technology Stack

This project uses:
- Python 3.11 with FastAPI
- TypeScript with React
- pytest for testing
- GitHub Actions for CI/CD

## Repository Structure

\`\`\`text
project/
├── src/          # FastAPI application
├── frontend/     # React application
├── tests/        # Test suite
└── .github/      # CI/CD workflows
\`\`\`
```

### Step 7: Verify and Commit

**Verify installation:**

```bash
test -f AGENTS.md || echo "⚠️  AGENTS.md missing"
test -f .github/.activate-version || echo "⚠️  Version marker missing"
```

**Commit changes (with user approval):**

```bash
git add AGENTS.md .github/
git commit -m "chore: install Activate Copilot v1.5.0 (standard bundle)

Installed and customized for:
- Python 3.11 + FastAPI
- TypeScript + React
"
```

### Step 8: Provide Next Steps

```text
✅ Activate Copilot v1.5.0 installed successfully!

Next steps:

1. Review AGENTS.md and customize for your workflow
2. Try: "@workspace what are our coding standards?"
3. Open a Python file to test instruction activation

To update later: "@workspace /activate update"

Documentation: https://github.com/adhocteam/activate-copilot
```

## Update Workflow

For updates, check current version first:

```bash
CURRENT=$(cat .github/.activate-version 2>/dev/null || echo "none")
LATEST=$(gh release view --repo adhocteam/activate-copilot --json tagName -q .tagName)

if [[ "$CURRENT" == "$LATEST" ]]; then
    echo "✓ Already on latest version ($CURRENT)"
    exit 0
fi
```

Then follow steps 3-8, being careful to merge rather than replace AGENTS.md.

## Error Handling

- **No write permission**: Inform user, exit gracefully
- **No gh CLI**: Provide manual download link
- **Network error**: Suggest downloading release manually
- **Existing AGENTS.md**: Always backup before replacing

## Examples

**Basic install:**

```text
User: @workspace /activate install

Agent: I'll install Activate Copilot for you.

[Analyzes repo, recommends bundle, installs]

✅ Activate Copilot v1.5.0 installed!
```

**Specify bundle:**

```text
User: @workspace /activate install full

Agent: Installing the full bundle with agents and skills...

[Proceeds with installation]
```

**Update:**

```text
User: @workspace /activate update

Agent: Checking for updates...

Current: v1.3.0
Latest: v1.5.0

What's new:
- Added TypeScript instructions
- Enhanced security checklist

Update now?
```

## Notes for Agents

- Show progress at each step
- Ask permission before committing
- Always backup before replacing files
- Be transparent about what you're doing
- Fail gracefully with helpful error messages

## Related

- ADR-001: Agent, Instruction, and Skill File Hierarchy
- ADR-002: GitHub Releases Distribution (V2 evolution)
- Issue #70: Add /activate installer skill
