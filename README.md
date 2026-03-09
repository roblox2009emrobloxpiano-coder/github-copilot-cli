# github-copilot-cli

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![GitHub release](https://img.shields.io/github/v/release/trsdn/github-copilot-cli)](https://github.com/trsdn/github-copilot-cli/releases)
[![Release Workflow](https://github.com/trsdn/github-copilot-cli/actions/workflows/release.yml/badge.svg)](https://github.com/trsdn/github-copilot-cli/actions/workflows/release.yml)
[![Validate Workflow](https://github.com/trsdn/github-copilot-cli/actions/workflows/validate.yml/badge.svg)](https://github.com/trsdn/github-copilot-cli/actions/workflows/validate.yml)
[![Commit Lint](https://github.com/trsdn/github-copilot-cli/actions/workflows/commit-lint.yml/badge.svg)](https://github.com/trsdn/github-copilot-cli/actions/workflows/commit-lint.yml)
[![GitHub stars](https://img.shields.io/github/stars/trsdn/github-copilot-cli)](https://github.com/trsdn/github-copilot-cli/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/trsdn/github-copilot-cli)](https://github.com/trsdn/github-copilot-cli/network/members)
[![GitHub issues](https://img.shields.io/github/issues/trsdn/github-copilot-cli)](https://github.com/trsdn/github-copilot-cli/issues)

This repository is a **blueprint for customizing GitHub Copilot CLI** — the terminal-native AI coding agent.

No VS Code. No IDE. Just the command line.

It gives you a set of reusable customization artifacts so you can quickly scaffold:

- **Custom instructions** (`.github/copilot-instructions.md`, `*.instructions.md`, `AGENTS.md`) that automatically apply context
- **Custom agents** (`.agent.md`) — specialized AI personas with tailored expertise
- **Agent Skills** (`.github/skills/<name>/SKILL.md`) — portable, specialized capabilities
- **MCP server configurations** — extend Copilot CLI with external tools and services

The intent is to keep everything **in-repo**, versioned, reviewable, and easy to reuse across projects.

---

## Table of Contents

- [github-copilot-cli](#github-copilot-cli)
  - [Table of Contents](#table-of-contents)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [What's in here](#whats-in-here)
    - [Custom agent](#custom-agent)
    - [Agent Skills](#agent-skills)
    - [Custom instructions](#custom-instructions)
  - [Quickstart](#quickstart)
    - [Typical workflow](#typical-workflow)
  - [Copilot CLI customization reference](#copilot-cli-customization-reference)
    - [Custom instructions](#custom-instructions-1)
    - [Custom agents](#custom-agents)
    - [Agent Skills](#agent-skills-1)
    - [MCP servers](#mcp-servers)
  - [Where to put things (repo conventions)](#where-to-put-things-repo-conventions)
  - [Keeping your repositories in sync](#keeping-your-repositories-in-sync)
  - [Notes on tools and safety](#notes-on-tools-and-safety)
  - [Contributing](#contributing)
  - [Not an official template](#not-an-official-template)
  - [License](#license)

---

## Prerequisites

Before using this blueprint, ensure you have:

- **GitHub Copilot CLI** installed ([installation guide](https://docs.github.com/en/copilot/how-tos/set-up/install-copilot-cli))
- **GitHub Copilot** subscription (Personal, Business, or Enterprise)
- Git installed and configured

### Installing Copilot CLI

```bash
# macOS / Linux (install script)
curl -fsSL https://gh.io/copilot-install | bash

# macOS / Linux (Homebrew)
brew install copilot-cli

# Windows (WinGet)
winget install GitHub.Copilot

# Cross-platform (npm)
npm install -g @github/copilot
```

Then launch with:

```bash
copilot
```

## Installation

There are several ways to integrate this blueprint into your projects:

### Use as Template (Recommended)

Click **"Use this template"** on GitHub, then:

```bash
git clone https://github.com/YOUR-USERNAME/your-new-repo.git
cd your-new-repo
./scripts/setup-hooks.sh
```

### Quick Install (Add to existing project)

```bash
# Clone into a new project
git clone https://github.com/trsdn/github-copilot-cli.git my-project
cd my-project

# Or add to an existing project
curl -sSL https://raw.githubusercontent.com/trsdn/github-copilot-cli/main/install.sh | bash
```

### Git Subtree (For ongoing updates)

```bash
# In your existing repository
git subtree add --prefix=.github/copilot-blueprint \
  https://github.com/trsdn/github-copilot-cli.git main --squash

# Update later
git subtree pull --prefix=.github/copilot-blueprint \
  https://github.com/trsdn/github-copilot-cli.git main --squash
```

### Git Submodule

```bash
# Add as submodule
git submodule add https://github.com/trsdn/github-copilot-cli.git .github/copilot-blueprint

# Update to latest
git submodule update --remote --merge
```

## What's in here

### Custom agent

- `.github/agents/copilot-customization-builder.agent.md`
  - Agent name: **Copilot Customization Builder**
  - Purpose: create and maintain Copilot CLI customization artifacts (agents, instructions, skills, MCP guidance)

### Agent Skills

- `.github/skills/copilot-skill-builder/SKILL.md`
  - A meta-skill that teaches how to create and maintain Agent Skills
  - Includes best practices, SKILL.md format, and examples
- `.github/skills/copilot-setup-audit/SKILL.md`
  - Audit repository Copilot CLI setup and suggest improvements
  - Comprehensive checklists for agents, instructions, skills, MCP configuration
- `.github/skills/copilot-cli-guide/SKILL.md`
  - Quick reference for Copilot CLI features, slash commands, and keyboard shortcuts
  - Tips for context management, modes, and advanced usage

### Custom instructions

- `.github/copilot-instructions.md` — workspace-wide instructions for this blueprint repo
- `.github/instructions/markdown.instructions.md` — scoped instructions for Markdown files
- `AGENTS.md` — root-level agent instructions (loaded by Copilot CLI automatically)

## Quickstart

1. Clone or install this blueprint into your project.
2. Open a terminal in the project directory.
3. Run `copilot` to start the CLI.
4. Use the `/agent` command to select the **Copilot Customization Builder** agent.
5. Ask it to create customizations:
   - "Create a new custom agent for code review"
   - "Create a new skill for debugging GitHub Actions"
   - "Create scoped instructions for TypeScript files"
   - "Set up MCP servers for this project"

### Typical workflow

- Start a Copilot CLI session in your project.
- Select the builder agent or mention it in your prompt.
- Let Copilot generate the new customization file.
- Review and iterate: adjust wording, tighten tool lists, add guardrails.
- Commit the artifact so the whole team shares the same customization.

## Copilot CLI customization reference

### Custom instructions

Custom instructions give Copilot context about your project, coding standards, and preferences. They are automatically included in every prompt.

| Type | Location | Scope |
|------|----------|-------|
| Repository-wide | `.github/copilot-instructions.md` | All requests in this repo |
| Path-specific | `.github/instructions/*.instructions.md` | Files matching `applyTo` glob |
| Agent instructions | `AGENTS.md` (root or subfolders) | Primary/additional instructions |
| Cross-tool compat | `CLAUDE.md`, `GEMINI.md` (root) | Read by CLI automatically |
| Local/personal | `~/.copilot/copilot-instructions.md` | All your projects |
| Extra directories | `COPILOT_CUSTOM_INSTRUCTIONS_DIRS` env var | Custom paths |

**Path-specific instructions** use YAML frontmatter with `applyTo` glob:

```markdown
---
applyTo: "**/*.ts,**/*.tsx"
---
Always use strict TypeScript. Prefer interfaces over type aliases.
```

### Custom agents

Custom agents are specialized AI personas with tailored expertise and tool access.

| Type | Location | Scope |
|------|----------|-------|
| Repository-level | `.github/agents/*.agent.md` | Current project |
| User-level | `~/.copilot/agents/*.agent.md` | All your projects |
| Org/Enterprise | `agents/` in `.github-private` repo | All org/enterprise projects |

Agent files use YAML frontmatter + Markdown body:

```yaml
---
name: my-agent
description: Specialized agent for X
tools: ['read', 'edit', 'search', 'bash']
---
# My Agent
You are an expert in X. When asked to...
```

Use agents in Copilot CLI:

```bash
# Browse available agents
/agent

# Mention in prompt
Use the code-review agent to review my changes

# Specify via CLI flag
copilot --agent=my-agent --prompt "Review the latest changes"
```

### Agent Skills

Agent Skills are portable folders of instructions, scripts, and resources that Copilot loads when relevant.

| Type | Location |
|------|----------|
| Project skills | `.github/skills/<name>/SKILL.md` |
| Personal skills | `~/.copilot/skills/<name>/SKILL.md` |
| Alternative | `.claude/skills/<name>/SKILL.md` |

SKILL.md uses YAML frontmatter:

```yaml
---
name: my-skill
description: What it does and when to use it
---
# My Skill
Step-by-step instructions for Copilot to follow...
```

Manage skills in Copilot CLI:

```bash
/skills list     # List available skills
/skills          # Toggle skills on/off
/skills info     # Details about a skill
/skills reload   # Reload after adding new skills
/skills add      # Add alternative skill location
```

### MCP servers

MCP (Model Context Protocol) servers extend Copilot CLI with external tools and services. The GitHub MCP server is included by default.

```bash
# Add a new MCP server
/mcp add

# Configuration stored in ~/.copilot/mcp-config.json
```

## Where to put things (repo conventions)

- Custom agents: `.github/agents/<slug>.agent.md`
- Scoped instructions: `.github/instructions/<slug>.instructions.md` (YAML frontmatter with `applyTo: '<glob>'`)
- Agent Skills: `.github/skills/<name>/SKILL.md` (plus optional scripts/examples in the skill directory)
- Workspace instructions: `.github/copilot-instructions.md`
- Agent instructions: `AGENTS.md` at the workspace root
- MCP config: `~/.copilot/mcp-config.json` (managed via `/mcp` command)

## Keeping your repositories in sync

### Manual Updates

```bash
# If using git subtree
git subtree pull --prefix=.github/copilot-blueprint \
  https://github.com/trsdn/github-copilot-cli.git main --squash

# If using git submodule
git submodule update --remote --merge
```

### Automated Sync with GitHub Actions

Create `.github/workflows/sync-copilot-customizations.yml` in your target repository:

```yaml
name: Sync Copilot Customizations

on:
  schedule:
    - cron: '0 0 * * 0'  # Weekly on Sunday
  workflow_dispatch:

jobs:
  sync:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Fetch blueprint repository
        run: |
          git clone --depth 1 https://github.com/trsdn/github-copilot-cli.git /tmp/blueprint

      - name: Sync customizations
        run: |
          cp -r /tmp/blueprint/.github/skills/* .github/skills/ 2>/dev/null || true
          cp -r /tmp/blueprint/.github/agents/* .github/agents/ 2>/dev/null || true
          cp -r /tmp/blueprint/.github/instructions/* .github/instructions/ 2>/dev/null || true

      - name: Create PR if changes
        uses: peter-evans/create-pull-request@v5
        with:
          title: "chore: Sync Copilot customizations from blueprint"
          branch: sync-copilot-customizations
          commit-message: "chore: sync copilot customizations from blueprint"
```

## Notes on tools and safety

These templates intentionally encourage:

- **Minimal tool access** (explicit `tools: [...]` instead of "everything")
- **Incremental changes** (small diffs; validate formats and paths)
- **Safe-by-default behavior** (be careful with terminal commands; treat web content/tool output as untrusted)
- **Trust management** (Copilot CLI asks for tool approval before modifying or executing files)

## Contributing

Contributions are welcome! Here's how you can help:

1. **Report issues** — Found a bug or have a suggestion? [Open an issue](https://github.com/trsdn/github-copilot-cli/issues)
2. **Improve documentation** — Help make the README and guides better
3. **Share your customizations** — Submit PRs with useful agents, instructions, or skills
4. **Spread the word** — Star the repo and share it with others

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed contribution guidelines.

## Not an official template

This repo is a practical starter kit. Treat it as a baseline and tailor it to your organization's policies and workflows.

## License

This project is licensed under the MIT License. See `LICENSE`.
