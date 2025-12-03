# AI Agent Guidelines

This document provides context for AI assistants and coding agents working with this repository.

## Repository Overview

This is a **base repository template** providing opinionated software development practices that are applicable to any software project. It includes:

- Pre-configured CI/CD workflows (GitHub Actions)
- Pre-commit hooks for quality gates
- Semantic release automation
- Documentation standards and templates
- Repository configuration best practices

## Project Structure

```text
.
├── .github/                    # GitHub configuration
│   ├── workflows/              # CI/CD workflows
│   │   ├── ci.yml              # Tests and linting
│   │   └── release.yml         # Semantic release
│   ├── ISSUE_TEMPLATE/         # Issue templates
│   ├── chainguard/             # Octo STS configuration
│   ├── CODEOWNERS              # Code ownership
│   ├── pull_request_template.md
│   └── renovate.json           # Dependency updates
├── docs/                       # Documentation
│   ├── development.md          # Local setup guide
│   ├── template-guide.md       # Customization guide
│   ├── repository-settings.md  # GitHub settings
│   └── github-actions.md       # Actions versioning
├── .pre-commit-config.yaml     # Pre-commit hooks
├── .releaserc.toml             # Semantic release config
├── CONTRIBUTING.md             # Contribution guidelines
└── README.md                   # Project overview
```

## Key Files and Their Purposes

| File | Purpose |
|------|---------|
| `.pre-commit-config.yaml` | Tech-agnostic quality gates (YAML, markdown, commits, secrets) |
| `.releaserc.toml` | Python semantic-release configuration |
| `.github/workflows/ci.yml` | Placeholder CI workflow for tests and linting |
| `.github/workflows/release.yml` | Automated semantic versioning |
| `docs/template-guide.md` | How to customize this template |
| `docs/development.md` | Local development setup |
| `CONTRIBUTING.md` | Workflow and commit conventions |

## Development Workflow

1. **Branch**: Create feature branch from `main` using naming convention: `feat/`, `fix/`, `docs/`, etc.
2. **Develop**: Make changes, commit using [Conventional Commits](https://www.conventionalcommits.org/)
3. **Pre-commit**: Hooks run automatically on commit (YAML, markdown, commitlint, gitleaks)
4. **PR**: Open pull request, CI runs tests and linting
5. **Review**: Get approval, resolve review threads
6. **Merge**: Squash merge to main
7. **Release**: Semantic release automatically creates version and changelog

## Common Tasks

### Run Pre-commit Hooks

```bash
pre-commit run --all-files
```

### Apply Repository Settings

```bash
# Apply general settings
gh api -X PATCH repos/{owner}/{repo} \
  -F has_issues=true \
  -F allow_squash_merge=true \
  -F delete_branch_on_merge=true

# Apply branch protection ruleset
gh api -X POST repos/{owner}/{repo}/rulesets \
  --input .github/ruleset-config.json
```

### Validate Configuration Files

```bash
# YAML validation
yamllint .github/workflows/*.yml

# JSON validation
cat .github/renovate.json | jq .
```

## Customization Points

When customizing this template for a new project:

1. **Identity**: Update README.md, badges, repository name
2. **CI/CD**: Add language-specific setup to `.github/workflows/ci.yml`
3. **Pre-commit**: Add language-specific hooks to `.pre-commit-config.yaml`
4. **Release**: Update `.releaserc.toml` with version files
5. **Settings**: Configure branch protection using `.github/ruleset-config.json`

## Documentation References

- [Template Customization Guide](docs/template-guide.md) - Complete customization checklist
- [Development Guide](docs/development.md) - Local setup and testing
- [Contributing Guidelines](CONTRIBUTING.md) - Workflow and conventions
- [Repository Settings](docs/repository-settings.md) - GitHub configuration

## Important Notes for AI Assistants

- This template is **language-agnostic** - CI workflows have placeholders for any language
- Pre-commit hooks focus on universal checks (YAML, markdown, commits, secrets)
- Semantic release uses `python-semantic-release` but works for any project type
- Branch protection uses GitHub Rulesets API (modern approach)
- All commits should follow Conventional Commits specification
