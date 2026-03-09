# Copilot Instructions

These instructions are automatically applied to every Copilot CLI session in this workspace.

## Project Context

This is a **GitHub Copilot CLI Customization Blueprint** — a template repository for bootstrapping
custom agents, instructions, skills, and MCP configurations for the terminal-native Copilot experience.

This blueprint is **CLI-only** — no VS Code, no IDE dependencies.

## Conventions

- All customization files live under `.github/` (agents, skills, instructions)
- Use **Conventional Commits** for all commit messages: `<type>(<scope>): <description>`
- Allowed types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert`
- Agent files: `.agent.md` with YAML frontmatter (`description` required, `name` and `tools` recommended)
- Skill files: `SKILL.md` in a named directory under `.github/skills/<name>/`
- Instruction files: `*.instructions.md` with YAML frontmatter (`applyTo` glob required)
- For cross-tool compatibility, also support `CLAUDE.md`, `GEMINI.md`, and `AGENTS.md` at repo root

## File Structure

```
.github/
├── agents/           # Custom agent profiles (.agent.md)
├── instructions/     # Scoped instruction files (*.instructions.md)
├── skills/           # Agent Skills (each in its own directory with SKILL.md)
├── workflows/        # GitHub Actions (release, validate, commit-lint)
└── copilot-instructions.md  # This file
AGENTS.md             # Root-level agent instructions
```

## Code Style

- Markdown: ATX-style headings, fenced code blocks with language identifiers
- YAML frontmatter: quote strings that contain special characters
- Shell scripts: use `set -e`, add color output, include usage help
- Keep lines under 120 characters where practical
