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

### Semantic Release Setup (First Release)

If you’re using python-semantic-release (PSR), start your project at an initial version of `0.0.0`.

Why: PSR only commits files that *change* during version stamping. If you start at your “first real”
version (e.g. `0.1.0`), then the release commit may not include your version file(s) or lockfile(s)
(because PSR has nothing to update), which is confusing during initial setup.

Examples:

- Python (`pyproject.toml`): set `project.version = "0.0.0"` and configure PSR `version_toml`.
- uv (`uv.lock`): run `uv lock` after stamping so the lockfile reflects the stamped version.

In practice:

- [ ] Set your package metadata version to `0.0.0`
- [ ] Configure PSR to stamp the version into that file
- [ ] Ensure your release process regenerates lockfiles (if applicable) so they get committed

> **Best Practice:** Always pin GitHub Actions to specific versions (e.g., `@v4`) for stability and security. Avoid `@latest` except for rapidly evolving actions where you commit to active monitoring.

### Pre-commit Hooks

- [ ] Review `.pre-commit-config.yaml`: add language-specific hooks and remove any that are not needed.
- [ ] Configure hook versions to match your project's requirements
- [ ] Run `pre-commit autoupdate` to update the hooks to the latest versions.

### Dependency Management

- [ ] Verify Renovate Bot is installed for your organization (if using dependency management)
- [ ] Review `.github/renovate.json` and customize it for your project.
- [ ] Run `npx --yes --package renovate -- renovate-config-validator` to validate the configuration.
- [ ] Review the initial onboarding PR and merge it if everything looks good.

### Documentation

- [ ] Update `README.md` with project-specific information
- [ ] Customize `CONTRIBUTING.md` with project-specific contribution guidelines
- [ ] Review and update issue templates in `.github/ISSUE_TEMPLATE/`
- [ ] Customize pull request template in `.github/pull_request_template.md`
- [ ] Update `docs/development.md` with project-specific setup instructions
- [ ] Update `docs/ARCHITECTURE.md` with your system architecture
- [ ] Update `AGENTS.md` with any specific instructions for AI assistants not covered by the other documentation.
- [ ] Remove any placeholders like `{OWNER}`, `{REPO}`, `{ORGANIZATION}`, `{TEAM_NAME}`, etc.
- [ ] Delete the CHANGELOG.md file if it exists. Semantic release will generate it automatically.
- [ ] Delete this file.

### Secrets and Authentication

The following may need to be configured at your organization level:

- [ ] Verify Octo STS is configured (for semantic-release workflow) - if using Chainguard
- [ ] Verify Renovate Bot GitHub App is installed (if `.github/renovate.json` exists)

### Repository Settings

- [ ] Apply general repository settings (see commands below)
- [ ] Enable branch protection for `main` branch using `.github/ruleset-config.json`
- [ ] Add Chainguard Octo STS to bypass list (if using semantic-release)
- [ ] Configure required status checks (CI workflows)
- [ ] Set up CODEOWNERS file if needed

**Apply settings via GitHub CLI:**

```bash
# General settings (squash merge only, auto-delete branches)
gh api -X PATCH repos/{owner}/{repo} \
  -F has_issues=true \
  -F has_wiki=true \
  -F allow_squash_merge=true \
  -F allow_merge_commit=false \
  -F allow_rebase_merge=false \
  -F delete_branch_on_merge=true

# Branch protection ruleset
gh api -X POST repos/{owner}/{repo}/rulesets \
  --input .github/ruleset-config.json
```

**Important:** If using semantic-release, add Chainguard Octo STS to the ruleset bypass list via GitHub UI: Settings → Rules → Rulesets → Edit → Bypass list → Add "Chainguard Octo-sts".

### Post-Customization Verification

After completing customization:

1. Run pre-commit hooks to verify all files pass: `pre-commit run --all-files`
2. Review branch protection settings are correctly configured
3. Create a conventional commit and push it to the main branch
4. Verify CI workflows pass on the main branch
5. Verify the semantic release workflow runs successfully and creates a new release
