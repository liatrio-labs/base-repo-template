# Base Repository Template

A GitHub template repository with opinionated developer experience, quality gates, and CI/CD automation ready for customization.

<!-- TODO: Update badge with your repository URL -->
<!-- [![CI Status](https://github.com/{OWNER}/{REPO}/actions/workflows/ci.yml/badge.svg)](https://github.com/{OWNER}/{REPO}/actions/workflows/ci.yml) -->

## Features

This template provides a proven foundation for new projects, including:

- **Pre-configured CI/CD**: GitHub Actions workflows for testing, linting, and semantic versioning
- **Quality gates**: Pre-commit hooks for YAML validation, markdown linting, and conventional commits
- **Automated releases**: Semantic versioning with changelog generation
- **Documentation standards**: Contribution guidelines, issue templates, and PR templates
- **AI-ready development**: AGENTS.md and architecture documentation for AI assistants

## Quick Start

### 1. Create Repository from Template

Click the **"Use this template"** button at the top of this repository, or use the GitHub CLI:

```bash
gh repo create my-new-project --template {OWNER}/{REPO} --private
cd my-new-project
```

### 2. Install Pre-commit

Install pre-commit for local quality gates:

```bash
# macOS
brew install pre-commit

# Ubuntu/Debian
sudo apt install pre-commit

# pip (all platforms)
pip install pre-commit
```

### 3. Set Up Pre-commit Hooks

```bash
pre-commit install
```

> Secret scanning is enforced with [Gitleaks](https://github.com/gitleaks/gitleaks). If the hook blocks a commit, remove the secret, rotate the credential, and rerun `pre-commit`.

### 4. Customize for Your Project

Follow the [Template Customization Guide](docs/template-guide.md) to adapt the template for your specific project:

- Update repository identity (README, badges, descriptions)
- Customize CI/CD workflows for your language/framework
- Add language-specific pre-commit hooks
- Configure branch protection and repository settings

## What's Included

### Pre-commit Hooks (Tech-Agnostic)

- YAML and TOML validation
- Markdown linting
- Trailing whitespace and EOF fixes
- Conventional commits enforcement
- Secret scanning (Gitleaks)

### CI/CD Workflows

- `ci.yml`: Placeholder for tests and linting (customize per language)
- `release.yml`: Semantic release automation

### Documentation

- Contributing guidelines with conventional commits
- Development setup guide
- Architecture documentation template
- Repository settings documentation

### Scripts

- `apply-repo-settings.sh`: Automate GitHub repository configuration
- `ruleset-config.json`: Branch protection configuration

## Documentation

- [Template Customization Guide](docs/template-guide.md) - Complete customization checklist
- [Contributing Guidelines](CONTRIBUTING.md) - Development workflow and conventions
- [Development Setup](docs/development.md) - Local setup and repository settings
- [Architecture](docs/ARCHITECTURE.md) - System architecture documentation
- [AI Agent Guidelines](AGENTS.md) - Context for AI assistants

## Customization Checklist

After creating a repository from this template:

- [ ] Update this README with your project information
- [ ] Update CI badges with your repository URLs
- [ ] Customize `.github/workflows/ci.yml` for your language
- [ ] Add language-specific pre-commit hooks
- [ ] Update `.github/chainguard/main-semantic-release.sts.yaml` subject pattern
- [ ] Update `.github/CODEOWNERS` with your team
- [ ] Configure branch protection rules
- [ ] Remove this checklist section
