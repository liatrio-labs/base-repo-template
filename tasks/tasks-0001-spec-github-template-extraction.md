# Task List: GitHub Template Repository Extraction

This task list breaks down the implementation of the specification defined in `0001-spec-github-template-extraction.md`. The goal is to extract a reusable GitHub template repository from `spec-driven-workflow` that preserves developer experience, tooling, and CI/CD automation while removing product-specific functionality.

## Relevant Files

**To be created in `open-source-template/`:**

- `.github/workflows/ci.yml` - Placeholder CI workflow with test and lint jobs
- `.github/workflows/release.yml` - Semantic release automation workflow
- `.github/workflows/claude.yml` - Claude Code AI integration workflow
- `.github/workflows/opencode-gpt-5-codex.yml` - OpenCode GPT-5 Codex workflow
- `.github/chainguard/main-semantic-release.sts.yaml` - Chainguard Octo STS configuration
- `.github/ISSUE_TEMPLATE/bug_report.yml` - Generalized bug report template
- `.github/ISSUE_TEMPLATE/feature_request.yml` - Generalized feature request template
- `.github/ISSUE_TEMPLATE/config.yml` - Issue template configuration
- `.github/pull_request_template.md` - Generalized PR template
- `.pre-commit-config.yaml` - Language-agnostic pre-commit hooks configuration
- `.markdownlint.yaml` - Markdown linting configuration
- `.gitignore` - Common ignore patterns for version control
- `README.md` - Template documentation with quick start and customization guide
- `CONTRIBUTING.md` - Contribution guidelines and workflow documentation
- `LICENSE` - Apache 2.0 license file
- `docs/development.md` - Development setup and best practices documentation
- `docs/repository-settings.md` - Documentation of captured repository settings and automation
- `scripts/apply-repo-settings.sh` - Optional automation script for applying repository settings via gh CLI

**Source files to reference from `~/Liatrio/repos/spec-driven-workflow/`:**

- `.github/workflows/ci.yml` - Source CI workflow to adapt
- `.github/workflows/release.yml` - Source semantic release workflow
- `.github/workflows/claude.yml` - Source Claude workflow
- `.github/workflows/opencode-gpt-5-codex.yml` - Source OpenCode workflow
- `.github/ISSUE_TEMPLATE/*` - Source issue templates to generalize
- `.github/pull_request_template.md` - Source PR template
- `.pre-commit-config.yaml` - Source pre-commit configuration
- `README.md` - Source README for structure reference
- `CONTRIBUTING.md` - Source contribution guidelines
- `LICENSE` - Apache 2.0 license to copy

### Notes

- All files will be created in the `/home/damien/Liatrio/repos/open-source-template/` directory
- Source repository is located at `~/Liatrio/repos/spec-driven-workflow/`
- Template should be language-agnostic; Python-specific tooling will be removed
- Pre-commit hooks will focus on language-agnostic checks (YAML, markdown, commitlint)
- CI/CD workflows will use placeholder commands with clear documentation for customization
- Repository settings automation (task 6.0) uses `gh api` to capture branch protection rules and settings

## Tasks

- [ ] 1.0 Create minimal repository structure with core configuration files
  - Demo Criteria: "Repository has all required directories (.github/, docs/) and base configuration files (.gitignore, LICENSE with Apache 2.0 and Liatrio attribution, .markdownlint.yaml); pre-commit hooks can be installed successfully"
  - Proof Artifact(s): "CLI: `tree -L 3` shows directory structure; `ls -la` shows .gitignore, LICENSE, .markdownlint.yaml; `cat LICENSE` shows Apache 2.0 with Liatrio copyright; `pre-commit install` succeeds"

- [ ] 2.0 Configure language-agnostic pre-commit hooks and code quality automation
  - Demo Criteria: "Pre-commit hooks install and run successfully on initial repository state; all hooks pass with no errors; configuration includes YAML validation, markdown linting, commitlint, trailing whitespace removal, end-of-file fixer, and commented autoupdate schedule"
  - Proof Artifact(s): "CLI: `pre-commit run --all-files` exits 0 with all hooks showing 'Passed' status; `grep 'autoupdate.*schedule.*quarterly' .pre-commit-config.yaml` finds commented schedule; all language-agnostic hooks present"

- [ ] 3.0 Create functional CI/CD workflow templates with placeholder jobs
  - Demo Criteria: "CI workflow YAML is valid and contains working placeholder jobs with clear customization documentation"
  - Proof Artifact(s): "CLI: `yamllint .github/workflows/ci.yml` passes; workflow contains placeholder echo commands; GitHub Actions validation passes (or local validation)"

- [ ] 4.0 Configure semantic release automation and AI workflow integrations
  - Demo Criteria: "Release workflow is configured for semantic-release starting at v0.1.0 with user reset documentation; Claude and OpenCode workflows are present with setup documentation; Octo STS configuration file exists with subject customization docs"
  - Proof Artifact(s): "Files exist: `.github/workflows/release.yml`, `.github/workflows/claude.yml`, `.github/workflows/opencode-gpt-5-codex.yml`, `.github/chainguard/main-semantic-release.sts.yaml`; YAML validation passes for all workflows; release.yml or docs mention v0.1.0 and versioning reset instructions"

- [ ] 5.0 Create comprehensive documentation and GitHub templates
  - Demo Criteria: "README explains template usage with quick start, documents GitHub secrets (CLAUDE_CODE_OAUTH_TOKEN, OPENAI_API_KEY_FOR_OPENCODE, Octo STS), and includes license change instructions; CONTRIBUTING covers development workflow and conventional commits; issue/PR templates are generalized; docs/development.md provides detailed setup guidance; all documentation links are valid; 'Template repository' setting enabled in GitHub"
  - Proof Artifact(s): "Files exist and render correctly: `README.md`, `CONTRIBUTING.md`, `docs/development.md`, `.github/ISSUE_TEMPLATE/*.yml`, `.github/pull_request_template.md`; all markdown passes linting; link checker validates all URLs; README contains secrets documentation and license change instructions; GitHub repository shows 'Template repository' badge/setting enabled"

- [ ] 6.0 Capture and document repository settings automation
  - Demo Criteria: "Repository settings from spec-driven-workflow are captured and documented; automation script/commands provided for applying settings; manual configuration steps documented as fallback"
  - Proof Artifact(s): "CLI: `gh api repos/liatrio/spec-driven-workflow` returns settings; `docs/repository-settings.md` contains captured settings and gh commands; optional `scripts/apply-repo-settings.sh` is idempotent"
