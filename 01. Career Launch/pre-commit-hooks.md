# pre-commit — hooks prêts à l'emploi

> Tous les hooks ci-dessous **existent réellement** (repo + `id` vérifiés). Les `rev:` sont des tags réels au moment de la rédaction — les mettre à jour avec `pre-commit autoupdate`.
> Chaque hook pointe vers un repo public : `https://github.com/<owner>/<repo>`.

---

## 1. Installer

```bash
# framework (choisir une méthode)
pipx install pre-commit      # recommandé (isole du python système)
pip install pre-commit       # sinon

# dans le repo concerné
pre-commit install                       # hook sur les commits
pre-commit install --hook-type commit-msg # hook sur les messages (commitlint)
pre-commit run --all-files               # 1ʳᵉ passe sur tout le repo
```

Le fichier de config va **à la racine** du repo : `.pre-commit-config.yaml`.

---

## 2. Socle recommandé (hygiène + secrets + messages)

```yaml
repos:
  # Hygiène de fichiers
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v6.0.0
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-yaml
      - id: check-json
      - id: check-merge-conflict
      - id: check-added-large-files
      - id: detect-private-key        # clés privées (RSA/SSH…)

  # Secrets
  - repo: https://github.com/gitleaks/gitleaks
    rev: v8.30.1
    hooks:
      - id: gitleaks

  # Messages de commit (Conventional Commits)
  - repo: https://github.com/alessandrojcm/commitlint-pre-commit-hook
    rev: v9.26.0
    hooks:
      - id: commitlint
        stages: [commit-msg]
        additional_dependencies: ['@commitlint/config-conventional']
```

> Pour `commitlint`, il faut aussi un `commitlint.config.js` à la racine :
> ```js
> module.exports = { extends: ['@commitlint/config-conventional'] };
> ```

---

## 3. Variante secrets : `detect-secrets`

Alternative/complément à gitleaks, avec un système de **baseline** (ignore les faux positifs déjà connus) :

```yaml
  - repo: https://github.com/Yelp/detect-secrets
    rev: v1.5.0
    hooks:
      - id: detect-secrets
        args: ['--baseline', '.secrets.baseline']
        exclude: package.lock.json
```

Créer la baseline une fois : `detect-secrets scan > .secrets.baseline`.

---

## 4. Hooks par langage (à ajouter selon le projet)

### Python — Ruff (linter + formateur)

```yaml
  - repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.16.4
    hooks:
      - id: ruff-check
        args: [--fix]
      - id: ruff-format
```
> ⚠️ L'ancien `id: ruff` a été renommé **`ruff-check`**.

### Shell — ShellCheck

```yaml
  - repo: https://github.com/koalaman/shellcheck-precommit
    rev: v0.11.0
    hooks:
      - id: shellcheck
```
> ⚠️ Ce hook officiel utilise **Docker** (`docker` doit être installé). Alternative sans Docker : `shellcheck-py/shellcheck-py`.

### Terraform / IaC

```yaml
  - repo: https://github.com/antonbabenko/pre-commit-terraform
    rev: v1.108.1
    hooks:
      - id: terraform_fmt
      - id: terraform_validate
      - id: terraform_checkov   # (l'ancien id `checkov` est déprécié)
```

### JavaScript / TypeScript — ESLint

```yaml
  - repo: https://github.com/pre-commit/mirrors-eslint
    rev: <à définir>   # exécuter pre-commit autoupdate
    hooks:
      - id: eslint
        additional_dependencies: ['eslint']
```
> ⚠️ Le mirror **prettier** (`pre-commit/mirrors-prettier`) est **déprécié** → préférer Prettier via Husky/npm côté projet.

---

## 5. Récap des hooks vérifiés

| Hook (`id`) | Repo | Ce qu'il fait |
|---|---|---|
| `trailing-whitespace` | pre-commit/pre-commit-hooks | Supprime les espaces en fin de ligne |
| `end-of-file-fixer` | pre-commit/pre-commit-hooks | Assure un unique retour à la ligne final |
| `check-yaml` / `check-json` | pre-commit/pre-commit-hooks | Valide la syntaxe YAML / JSON |
| `check-merge-conflict` | pre-commit/pre-commit-hooks | Bloque les marqueurs de conflit non résolus |
| `check-added-large-files` | pre-commit/pre-commit-hooks | Refuse les gros fichiers |
| `detect-private-key` | pre-commit/pre-commit-hooks | Détecte les clés privées |
| `mixed-line-ending` | pre-commit/pre-commit-hooks | Normalise les fins de ligne |
| `no-commit-to-branch` | pre-commit/pre-commit-hooks | Interdit de committer sur `main` |
| `gitleaks` | gitleaks/gitleaks | Détecte les secrets (clés, tokens, mdp) |
| `detect-secrets` | Yelp/detect-secrets | Détection de secrets avec baseline |
| `commitlint` | alessandrojcm/commitlint-pre-commit-hook | Valide le format des messages de commit |
| `ruff-check` / `ruff-format` | astral-sh/ruff-pre-commit | Lint + format Python |
| `shellcheck` | koalaman/shellcheck-precommit | Analyse les scripts shell |
| `black` / `black-jupyter` | psf/black-pre-commit-mirror | Formate Python (si pas Ruff) |
| `eslint` | pre-commit/mirrors-eslint | Lint JS/TS |
| `terraform_fmt` / `terraform_validate` / `terraform_checkov` | antonbabenko/pre-commit-terraform | Format, validation, sécu Terraform |
| `json`, `tag-pair`… | pre-commit/pygrep-hooks | Petits contrôles regex/markup |

---

## 6. Comportement & pièges

- Un hook en échec **bloque le commit**. Certains **corrigent** le fichier (whitespace, formatter) → refaire `git add` puis recommitter.
- Les hooks s'exécutent sur les fichiers **stagés**.
- Bypass : `git commit --no-verify` (à éviter) ou `SKIP=gitleaks git commit …` (skip ciblé).
- Un hook **côté client est contournable** → il ne remplace pas le **secret scanning + push protection** côté GitHub, ni un scan en **CI**.

---

## 7. Rejouer en CI (obligatoire pour garantir)

`.github/workflows/pre-commit.yml` :

```yaml
name: pre-commit
on: [push, pull_request]
jobs:
  pre-commit:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
      - uses: pre-commit/action@v3.0.1
```

---

## 8. Sources (pour vérifier soi-même)

- Framework : https://pre-commit.com
- Hooks officiels : https://github.com/pre-commit/pre-commit-hooks
- Gitleaks : https://github.com/gitleaks/gitleaks
- detect-secrets : https://github.com/Yelp/detect-secrets
- commitlint : https://github.com/alessandrojcm/commitlint-pre-commit-hook
- Ruff : https://github.com/astral-sh/ruff-pre-commit
- ShellCheck : https://github.com/koalaman/shellcheck-precommit
- Terraform : https://github.com/antonbabenko/pre-commit-terraform
