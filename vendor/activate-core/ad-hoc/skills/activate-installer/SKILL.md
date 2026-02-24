---
name: activate-installer
description: Installs Activate Copilot in a repository with intelligent customization. Use when asked to install, set up, or update Activate.
inputs:
  - name: tier
    description: 'minimal, standard, or advanced. Defaults to standard.'
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

Recommended tier: standard
```

### Step 2: Select Tier

Recommend tier based on analysis:

- **minimal**: Single language, simple project → security + general instructions
- **standard**: Multiple languages → adds ad-hoc instructions, skills, and agents
- **advanced**: Complex workflows → includes advanced tooling (when available)

Confirm with user:

```text
I recommend the 'standard' tier which includes:
- AGENTS.md (workflow guidance)
- Security and general instructions
- Python and TypeScript instructions
- Code review checklist

Which tier would you like?
```

### Step 3: Download Bundle

**Using GitHub CLI:**

```bash
gh release download \
  --repo adhocteam/activate-copilot \
  --pattern "activate-copilot-*.zip" \
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
unzip -q activate-copilot-*.zip -d "$TEMP_DIR"

# Show bundle layout and plugin payload
ls -la "$TEMP_DIR"
ls -la "$TEMP_DIR"/activate-copilot-*/plugins/activate-framework
```

Show user the file list:

```text
Bundle includes:

✓ install.mjs (root shim)
✓ docs/README.md
✓ plugins/activate-framework/manifest.json
✓ plugins/activate-framework/install.mjs
```

### Step 5: Install Files

Choose one installation path:

#### Option A: Script install (recommended)

```bash
cd "$TEMP_DIR"/activate-copilot-*
node install.mjs
```

This prompts for tier (`minimal`, `standard`, `advanced`) and target directory.

#### Option B: Manual install

**Handle existing AGENTS.md:**

If AGENTS.md exists, backup first:

```bash
mv AGENTS.md AGENTS.md.backup-$(date +%Y%m%d)
```

```bash
# Install core files
cp "$TEMP_DIR"/activate-copilot-*/plugins/activate-framework/AGENTS.md AGENTS.md
cp "$TEMP_DIR"/activate-copilot-*/plugins/activate-framework/instructions/security.instructions.md .github/instructions/
cp "$TEMP_DIR"/activate-copilot-*/plugins/activate-framework/instructions/general.instructions.md .github/instructions/
cp "$TEMP_DIR"/activate-copilot-*/plugins/activate-framework/prompts/*.prompt.md .github/prompts/

# Install ad-hoc files for standard tier
cp "$TEMP_DIR"/activate-copilot-*/plugins/activate-framework/instructions/code-review.instructions.md .github/instructions/
if [[ -f pyproject.toml ]]; then
    cp "$TEMP_DIR"/activate-copilot-*/plugins/activate-framework/instructions/python.instructions.md .github/instructions/
fi

if [[ -f package.json ]]; then
    cp "$TEMP_DIR"/activate-copilot-*/plugins/activate-framework/instructions/typescript.instructions.md .github/instructions/
fi

# Install advanced extras when requested
cp -r "$TEMP_DIR"/activate-copilot-*/plugins/activate-framework/skills .github/
cp -r "$TEMP_DIR"/activate-copilot-*/plugins/activate-framework/agents .github/

# Write version marker
cp "$TEMP_DIR"/activate-copilot-*/plugins/activate-framework/.activate-version .github/.activate-version
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
git commit -m "chore: install Activate Copilot v1.5.0 (standard tier)

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

[Analyzes repo, recommends tier, installs]

✅ Activate Copilot v1.5.0 installed!
```

**Specify tier:**

```text
User: @workspace /activate install advanced

Agent: Installing the advanced tier from the single bundle...

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
