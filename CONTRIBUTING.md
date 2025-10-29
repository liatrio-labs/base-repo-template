# Contributing

## Adding Language-Specific Pre-commit Hooks

This template includes language-agnostic pre-commit hooks by default (YAML validation, markdown linting, conventional commits). To add hooks for your specific programming language, update `.pre-commit-config.yaml` with the appropriate hooks.

### JavaScript/TypeScript Example

```yaml
  - repo: https://github.com/pre-commit/mirrors-eslint
    rev: v9.0.0
    hooks:
      - id: eslint
        files: \.[jt]sx?$
        types: [file]
```

### Python Example

```yaml
  - repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.14.0
    hooks:
      - id: ruff-check
        args: [--fix, --exit-non-zero-on-fix]
      - id: ruff-format
```

### Go Example

```yaml
  - repo: https://github.com/golangci/golangci-lint
    rev: v1.55.0
    hooks:
      - id: golangci-lint
```

### Rust Example

```yaml
  - repo: https://github.com/doublify/pre-commit-rust
    rev: v1.0
    hooks:
      - id: fmt
      - id: clippy
```

## Enabling/Disabling Hooks

To skip a specific hook during commit:

```bash
SKIP=hook-id git commit -m "message"
```

To disable the `no-commit-to-branch` hook (if enabled locally):

```bash
SKIP=no-commit-to-branch git commit -m "message"
```
