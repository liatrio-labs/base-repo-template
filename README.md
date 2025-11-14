# Liatrio Open Source Template

A battle-tested GitHub template repository with opinionated developer experience, quality gates, and CI/CD automation ready for customization.

[![CI Status](https://github.com/liatrio-labs/open-source-project-template/actions/workflows/ci.yml/badge.svg)](https://github.com/liatrio-labs/open-source-project-template/actions/workflows/ci.yml)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://github.com/liatrio-labs/open-source-project-template/blob/main/LICENSE)

## Why Use This Template?

This template provides Liatrio teams with a proven foundation for new projects, including:

- **Pre-configured CI/CD**: GitHub Actions workflows for testing, linting, and semantic versioning
- **Quality gates**: Pre-commit hooks for YAML validation, markdown linting, and conventional commits
- **Automated releases**: Semantic versioning with changelog generation
- **Documentation standards**: Contribution guidelines, issue templates, and PR templates

## Quick Start

### 1. Create Repository from Template

Click the **"Use this template"** button at the top of this repository, or use the GitHub CLI:

```bash
gh repo create my-new-project --template liatrio-labs/open-source-project-template --public
cd my-new-project
```

### 2. Install Dependencies

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

Follow the [Template Customization Guide](docs/template-guide.md) to adapt the template for your specific project.

## Documentation

- [Template Customization Guide](docs/template-guide.md) - Complete customization checklist and feature documentation
- [Contributing Guidelines](CONTRIBUTING.md) - Development workflow, conventional commits, and pre-commit hooks
- [Code of Conduct](CODE_OF_CONDUCT.md) - Community expectations and reporting guidance
- [Development Setup](docs/development.md) - Local setup, environment variables, and repository settings

## Support

For questions or issues with this template:

- Open an issue in this repository
- Contact the Liatrio DevOps team

## License

Copyright 2025 Liatrio

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

<http://www.apache.org/licenses/LICENSE-2.0>

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
