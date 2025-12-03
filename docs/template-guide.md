# Template Customization Guide

This guide provides detailed instructions for customizing this base template for your project.

## Customization Checklist

After creating your repository from this template, follow the checklist below:

### Repository Configuration

- [ ] Update repository name and description in GitHub settings
- [ ] Update `README.md` with your project name, description, and badges
- [ ] Update `.github/chainguard/main-semantic-release.sts.yaml` with your repository path
- [ ] Review and customize `.gitignore` for your language/framework

### CI/CD Workflows

- [ ] Update `.github/workflows/ci.yml` workflow name if needed
- [ ] Add language-specific setup steps (Node.js, Python, Go, Rust, Java, etc.)
- [ ] Replace placeholder test and lint commands with your actual commands
- [ ] Update paths-ignore in workflows if needed
- [ ] Review `.github/workflows/release.yml` and customize build/release steps

> **Best Practice:** Always pin GitHub Actions to specific versions (e.g., `@v4`) for stability and security. Avoid `@latest` except for rapidly evolving actions where you commit to active monitoring.

### Pre-commit Hooks

- [ ] Review `.pre-commit-config.yaml` and add language-specific hooks
- [ ] See [CONTRIBUTING.md](../CONTRIBUTING.md) for examples (ESLint, Ruff, golangci-lint, etc.)
- [ ] Configure hook versions to match your project's requirements

### Documentation

- [ ] Update `README.md` with project-specific information
- [ ] Customize `CONTRIBUTING.md` with project-specific contribution guidelines
- [ ] Review and update issue templates in `.github/ISSUE_TEMPLATE/`
- [ ] Customize pull request template in `.github/pull_request_template.md`
- [ ] Update `docs/development.md` with project-specific setup instructions
- [ ] Update `docs/ARCHITECTURE.md` with your system architecture
- [ ] Remove or update `docs/repository-settings.md` - this file contains template-specific repository settings guidance and should be cleaned up after customization

### Secrets and Authentication

The following may need to be configured at your organization level:

- [ ] Verify Octo STS is configured (for semantic-release workflow) - if using Chainguard
- [ ] Verify Renovate Bot GitHub App is installed (if `.github/renovate.json` exists)

See [Required GitHub Secrets](#required-github-secrets) for details.

### Repository Settings

- [ ] Enable branch protection for `main` branch
- [ ] Configure required status checks (CI workflows)
- [ ] Set up CODEOWNERS file if needed
- [ ] Review repository settings (Issues, Wikis, Discussions, etc.)

See [docs/development.md](development.md) for recommended repository settings.

### Post-Customization Verification

After completing customization:

1. Run pre-commit hooks to verify all files pass: `pre-commit run --all-files`
2. Verify CI workflows pass on your first commit
3. Review branch protection settings are correctly configured
4. Test the semantic release workflow by creating a conventional commit

## Features

### Quality Automation

**Pre-commit hooks** enforce quality standards before code is committed:

- YAML syntax validation
- Markdown linting
- Conventional Commits validation
- Trailing whitespace removal
- End-of-file fixes

Add language-specific hooks for your project (linting, formatting, testing) by editing `.pre-commit-config.yaml`.

### CI/CD Pipelines

**GitHub Actions workflows** automate testing, linting, and releases:

- `ci.yml`: Runs tests and linters on every push and pull request
- `release.yml`: Automated semantic versioning and changelog generation

### Semantic Versioning

**Automated releases** using semantic-release:

- Analyzes commits using Conventional Commits
- Bumps version automatically (major.minor.patch)
- Generates CHANGELOG.md
- Creates GitHub releases

**Note:** This template starts at `v0.1.0` for demonstration. When starting your project:

1. Delete existing tags: `git tag -d $(git tag -l)`
2. Remove `CHANGELOG.md` if it exists
3. Your first release will start at the appropriate version based on your commit types

### Automated Dependency Management

**Renovate Bot** keeps dependencies up to date with conservative, controlled updates:

- Automatically creates pull requests for dependency updates
- Conservative configuration: no auto-merge, manual review required
- Rate-limited to prevent PR spam (`prHourlyLimit: 2`, `prConcurrentLimit: 10`)
- Scheduled updates run before 3am on Mondays (Pacific time)
- Dependency dashboard provides overview of all updates

**Installation:**

1. Install the [Renovate Bot GitHub App](https://github.com/apps/renovate)
2. Choose "All repositories" or "Select repositories" for your organization
3. Renovate will automatically detect the configuration file at `.github/renovate.json`
4. An onboarding PR will be created to confirm configuration

**Verification:**

To verify Renovate Bot is installed and active:

- **Using GitHub CLI:**
  - Check for Renovate-created PRs: `gh pr list --author "renovate[bot]" --limit 1`
  - Check organization installations: `gh api orgs/{org}/installations` and filter for Renovate app by app_slug: renovate
- **Using GitHub Web UI:**
  - Go to Repository Settings → Integrations → GitHub Apps
  - Verify "Renovate" appears in the installed apps list
  - Or check for PRs created by `renovate[bot]` user

**Note:** If `.github/renovate.json` exists but Renovate Bot is not installed, Renovate will not create dependency update PRs. Ensure the GitHub App is installed for Renovate to function.

**Configuration:**

The template includes a conservative Renovate configuration at `.github/renovate.json` that:

- Extends `config:recommended` with conservative overrides
- Requires manual review for all updates (no auto-merge)
- Groups updates by type (major vs. minor/patch)
- Limits PR creation rate to prevent overwhelming maintainers

**Note:** Update the `reviewers` and `assignees` fields in `.github/renovate.json` with your team's GitHub handles.

**Note:** Renovate uses a GitHub App for authentication and does not require any secrets to be configured.

### Verification Checklist

After customization, verify the following:

- [ ] All placeholder values (`{OWNER}`, `{REPO}`, `{ORGANIZATION}`, `{TEAM_NAME}`) are replaced
- [ ] Pre-commit hooks pass: `pre-commit run --all-files`
- [ ] CI workflow runs successfully
- [ ] Branch protection is configured
- [ ] CODEOWNERS file updated with your team
- [ ] Renovate Bot is installed (if using dependency management)

## Required GitHub Secrets

The following may need to be configured depending on your setup:

### Octo STS (Chainguard) - Optional

If using Chainguard Octo STS for semantic-release workflow authentication:

- Configure at the organization level via Chainguard Octo STS
- Provides short-lived tokens for GitHub Actions workflows
- Configuration file: `.github/chainguard/main-semantic-release.sts.yaml`
- **Important:** Update the `subject_pattern` in this file to match your repository

### Alternative: GitHub Token

If not using Octo STS, you can use a GitHub Personal Access Token or GitHub App token:

- Create a PAT with `contents: write` permissions
- Add as a repository secret named `GH_TOKEN`
- Update `.github/workflows/release.yml` to use the secret
