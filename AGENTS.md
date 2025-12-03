# AI Agent Guidelines

<!-- Context marker for AI assistants: 🤖 -->

This document provides context for AI assistants and coding agents working with this repository.

## Repository Overview

This is a **base repository template** providing opinionated software development practices applicable to any software project:

- Pre-configured CI/CD workflows (GitHub Actions)
- Pre-commit hooks for quality gates
- Semantic release automation
- Documentation standards and templates
- Repository configuration best practices

## Project Structure

```text
.
├── .github/
│   ├── workflows/
│   │   ├── ci.yml              # Tests and linting (placeholder)
│   │   └── release.yml         # Semantic release
│   ├── ISSUE_TEMPLATE/         # Issue templates
│   ├── chainguard/             # Octo STS configuration
│   ├── ruleset-config.json     # Branch protection config
│   ├── CODEOWNERS
│   ├── pull_request_template.md
│   └── renovate.json           # Dependency updates
├── docs/
│   ├── ARCHITECTURE.md         # System architecture template
│   ├── development.md          # Local setup guide
│   ├── template-guide.md       # Customization checklist
│   └── repository-settings.md  # GitHub settings reference
├── .pre-commit-config.yaml     # Quality gates
├── .releaserc.toml             # Semantic release config
├── CONTRIBUTING.md             # Workflow and conventions
├── AGENTS.md                   # This file
└── README.md                   # Project overview
```

## Key Files

| File | Purpose |
|------|---------|
| `.pre-commit-config.yaml` | Tech-agnostic quality gates (YAML, markdown, commits, secrets) |
| `.releaserc.toml` | Semantic release configuration |
| `.github/workflows/ci.yml` | CI workflow with language placeholders |
| `.github/ruleset-config.json` | Branch protection ruleset for `gh api` |
| `docs/template-guide.md` | Customization checklist |
| `CONTRIBUTING.md` | Commit conventions and workflow |

## Quick Reference

**Run quality checks:**

```bash
pre-commit run --all-files
```

**Apply branch protection:**

```bash
gh api -X POST repos/{owner}/{repo}/rulesets --input .github/ruleset-config.json
```

For detailed workflows and conventions, see:

- [CONTRIBUTING.md](CONTRIBUTING.md) - Development workflow, commit conventions, pre-commit examples
- [docs/development.md](docs/development.md) - Local setup, testing, repository settings
- [docs/template-guide.md](docs/template-guide.md) - Complete customization checklist

## Important Notes for AI Assistants

- **Language-agnostic**: CI workflows have placeholders for any language
- **Pre-commit**: Universal checks only (YAML, markdown, commits, secrets)
- **Semantic release**: Uses `python-semantic-release` but works for any project
- **Branch protection**: Uses GitHub Rulesets API (modern approach)
- **Commits**: Must follow [Conventional Commits](https://www.conventionalcommits.org/)
- **Pin actions**: Always pin GitHub Actions to specific versions (e.g., `@v4`)
