# AGENTS.md

This file provides guidance to AI coding agents when working with code in this repository.

## Repository Overview

This is a personal profile repository for Fouad Ait Ouahmad, focused on cybersecurity (offensive security, agentic security). It serves as a public portfolio and professional presence on GitHub.

## Commit Convention

We follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<scope>): <description>

[optional body]
[optional footer]
```

Types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`

Example:
```
feat(readme): add project badges section
```

## Pre-commit Hooks

This repo uses [pre-commit](https://pre-commit.com/) with the following hooks:

- **Hygiene**: trailing whitespace, end-of-file, YAML/JSON validation, merge conflict detection, large file detection, private key detection
- **Secrets**: gitleaks (detects API keys, tokens, passwords)
- **Commit messages**: commitlint (enforces Conventional Commits)

### Setup

```bash
pip install pre-commit
pre-commit install
pre-commit install --hook-type commit-msg
```

### Run manually

```bash
pre-commit run --all-files
```

## Branching

- `main` — production-ready profile content
- Feature branches: `feat/<description>`, `fix/<description>`
- Always create a Pull Request to merge into `main`

## Security

- Never commit secrets, credentials, or `.env` files
- Use gitleaks to scan for secrets before committing
- Keep dependencies updated (Dependabot enabled)
