# Repository Settings

This document describes recommended repository settings captured from the `spec-driven-workflow` repository, along with automation commands and manual configuration steps.

## Table of Contents

- [Captured Settings](#captured-settings)
- [Automated Configuration](#automated-configuration)
- [Manual Configuration](#manual-configuration)
- [Branch Protection Rules](#branch-protection-rules)

## Captured Settings

The following settings were captured from `liatrio-labs/spec-driven-workflow` repository:

### General Settings

```json
{
  "has_issues": true,
  "has_wiki": true,
  "has_discussions": false,
  "allow_squash_merge": true,
  "allow_merge_commit": true,
  "allow_rebase_merge": true,
  "delete_branch_on_merge": false
}
```

### Recommended Settings for Template

- **Issues**: Enabled (for bug tracking and feature requests)
- **Wiki**: Enabled (for additional documentation)
- **Discussions**: Disabled by default (enable if needed for community Q&A)
- **Squash merge**: Enabled (recommended for clean history)
- **Merge commits**: Enabled (preserves commit history when needed)
- **Rebase merge**: Enabled (for linear history)
- **Delete branch on merge**: **Enabled** (recommended - keeps repository clean)

### Branch Protection

The source repository (`spec-driven-workflow`) does not have branch protection enabled on `main`. However, for production projects, we **strongly recommend** enabling branch protection with the settings described in the [Branch Protection Rules](#branch-protection-rules) section below.

## Automated Configuration

### Prerequisites

- [GitHub CLI (`gh`)](https://cli.github.com/) installed and authenticated
- Repository admin access

### Apply General Settings

```bash
# Replace {owner} and {repo} with your repository details
# Example: owner=liatrio, repo=my-new-project

# Apply general repository settings
gh api -X PATCH repos/{owner}/{repo} \
  -F has_issues=true \
  -F has_wiki=true \
  -F has_discussions=false \
  -F allow_squash_merge=true \
  -F allow_merge_commit=true \
  -F allow_rebase_merge=true \
  -F delete_branch_on_merge=true
```

### Apply Branch Protection Rules

```bash
# Enable branch protection on main branch
# This ensures code quality and prevents accidental force pushes

gh api -X PUT repos/{owner}/{repo}/branches/main/protection \
  --input - <<'EOF'
{
  "required_status_checks": {
    "strict": true,
    "contexts": ["test", "lint"]
  },
  "enforce_admins": false,
  "required_pull_request_reviews": {
    "dismissal_restrictions": {},
    "dismiss_stale_reviews": true,
    "require_code_owner_reviews": false,
    "required_approving_review_count": 1
  },
  "restrictions": null,
  "allow_force_pushes": false,
  "allow_deletions": false,
  "required_conversation_resolution": true
}
EOF
```

### Verify Settings

```bash
# Fetch current repository settings
gh api repos/{owner}/{repo} | jq '{
  has_issues,
  has_wiki,
  has_discussions,
  allow_squash_merge,
  allow_merge_commit,
  allow_rebase_merge,
  delete_branch_on_merge
}'

# Fetch branch protection settings
gh api repos/{owner}/{repo}/branches/main/protection | jq .
```

## Manual Configuration

If you prefer to configure settings via the GitHub web interface:

### General Repository Settings

1. Navigate to your repository on GitHub
2. Click **Settings** (gear icon) in the repository menu
3. Go to **General** section

#### Features

- ✓ **Issues**: Check to enable bug tracking
- ✓ **Wikis**: Check to enable wiki documentation
- ☐ **Discussions**: Uncheck by default (enable if needed)
- ☐ **Projects**: Optional - enable if using GitHub Projects

#### Pull Requests

Under "Pull Requests" section:

- ✓ **Allow squash merging**: Check (recommended)
  - Optionally: ✓ Default to pull request title and commit details
- ✓ **Allow merge commits**: Check
  - Optionally: ✓ Default to pull request title and description
- ✓ **Allow rebase merging**: Check
- ✓ **Automatically delete head branches**: Check (recommended)

#### Template Repository

If this repository is intended as a template:

- ✓ **Template repository**: Check this box to allow users to create repositories from this template

### Branch Protection Rules

1. Navigate to **Settings** → **Branches**
2. Under "Branch protection rules", click **Add rule** or **Add classic branch protection rule**
3. Branch name pattern: `main`
4. Configure the protection settings (see below)
5. Click **Create** to save the branch protection rule

#### Protection Settings

**Protect matching branches:**

- ✓ **Require a pull request before merging**
  - ✓ **Require approvals**: 1
  - ✓ **Dismiss stale pull request approvals when new commits are pushed**
  - ☐ **Require review from Code Owners** (enable if you have CODEOWNERS file)

- ✓ **Require status checks to pass before merging**
  - ✓ **Require branches to be up to date before merging**
  - Add status checks: `test`, `lint` (match your CI job names)

- ✓ **Require conversation resolution before merging**

- ☐ **Require signed commits** (optional, recommended for high-security projects)

- ☐ **Require linear history** (optional, enforces rebase/squash merges)

- ☐ **Require deployments to succeed before merging** (if applicable)

- ☐ **Lock branch** (do not enable - prevents all pushes)

- ☐ **Do not allow bypassing the above settings** (optional, applies rules to admins)

- ☐ **Allow force pushes** (do not enable)

- ☐ **Allow deletions** (do not enable)

### Additional Recommended Settings

#### Code Security and Analysis

Navigate to **Settings** → **Code security and analysis**

Recommended settings:

- ✓ **Dependency graph**: Enable
- ✓ **Dependabot alerts**: Enable
- ✓ **Dependabot security updates**: Enable
- ☐ **Dependabot version updates**: Optional - enable to auto-update dependencies
- ✓ **Code scanning**: Enable if using GitHub Advanced Security

#### Secrets and Variables

Navigate to **Settings** → **Secrets and variables** → **Actions**

Required organization-level secrets (configured by Liatrio administrators):

- `CLAUDE_CODE_OAUTH_TOKEN` - For Claude Code workflow
- `OPENAI_API_KEY_FOR_OPENCODE` - For OpenCode GPT-5 Codex workflow
- Octo STS configuration - For semantic-release workflow

Repository-specific secrets (if needed):

- Add any project-specific API keys, tokens, or credentials here
- Never commit secrets to version control

## Branch Protection Rules

### Recommended Configuration

The following branch protection configuration is recommended for all production projects:

#### Required Status Checks

- **Require status checks to pass**: Yes
- **Require branches to be up to date**: Yes
- **Status checks**:
  - `test` (from CI workflow)
  - `lint` (from CI workflow)

#### Pull Request Reviews

- **Require approvals**: 1 minimum
- **Dismiss stale reviews**: Yes
- **Require review from Code Owners**: Optional (if CODEOWNERS file exists)

#### Additional Rules

- **Require conversation resolution**: Yes
- **Require signed commits**: Optional (recommended for compliance)
- **Require linear history**: Optional (enforces clean history)
- **Allow force pushes**: No
- **Allow deletions**: No

### Testing Branch Protection

Before applying to production, test branch protection rules:

1. Create a test branch: `git checkout -b test/branch-protection`
2. Make a commit and push: `git push -u origin test/branch-protection`
3. Open a pull request
4. Verify that:
   - CI checks run automatically
   - Merge is blocked until CI passes
   - At least one approval is required
   - Branch must be up to date before merging

## Troubleshooting

### Common Issues

#### gh CLI Not Authenticated

```bash
# Authenticate with GitHub
gh auth login

# Verify authentication
gh auth status
```

#### Insufficient Permissions

- Ensure you have **admin** access to the repository
- Organization-level settings may require organization owner permissions

#### Branch Protection Conflicts

- If branch protection fails to apply, check for conflicting rules
- Remove existing rules before applying new ones:

```bash
gh api -X DELETE repos/{owner}/{repo}/branches/main/protection
```

#### Status Checks Not Available

- Ensure CI workflows have run at least once
- Status check names must match exactly (case-sensitive)
- Wait for CI to complete before adding as required check

## Additional Resources

- [GitHub REST API Documentation](https://docs.github.com/en/rest)
- [Branch Protection Rules Documentation](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches)
- [GitHub CLI Manual](https://cli.github.com/manual/)
- [Repository Settings Best Practices](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features)
