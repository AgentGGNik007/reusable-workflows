# reusable-workflows

![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-reusable-2088FF?logo=githubactions&logoColor=white)
![git-cliff](https://img.shields.io/badge/changelog-git--cliff-orange)

Template-Repository mit wiederverwendbaren GitHub-Actions-Workflows für **Changelog-Generierung** (via [git-cliff](https://git-cliff.org)) und **Issue-Management**. Einmal sauber definiert, in allen Projekten und Organisationen einheitlich nutzbar.

CI/CD-Pipelines sind bewusst nicht Teil dieses Repos. Sie sind projektspezifisch und liegen im jeweiligen Repository.

## Inhalt

| Datei | Zweck |
|-------|-------|
| `.github/workflows/changelog.yml` | Generiert `CHANGELOG.md` aus Conventional Commits mit git-cliff |
| `.github/workflows/issues.yml` | Issue-Automatisierung (z. B. Labeling) |
| `cliff.toml` | Standard-Konfiguration für git-cliff |

## Verwendung

Workflow aus einem anderen Repository aufrufen:

```yaml
name: Changelog

on:
  push:
    tags: ["v*"]

jobs:
  changelog:
    uses: AgentGGNik007/reusable-workflows/.github/workflows/changelog.yml@v1
    with:
      config: cliff.toml
```

Immer auf einen Tag (`@v1`) oder Commit-SHA pinnen, nicht auf `@main`.

## Voraussetzungen

- Commits folgen den [Conventional Commits](https://www.conventionalcommits.org) (`feat:`, `fix:`, `docs:` …)
- Eine `cliff.toml` im aufrufenden Repo (Vorlage liegt in diesem Repo)
- Für Aufrufe aus anderen Repos: Quell-Repo public oder unter *Settings → Actions → General → Access* freigegeben


## Konventionen

- Dateinamen: `<zweck>.yml`, kebab-case
- Jeder Input und jedes Secret ist mit `description` dokumentiert
- Minimale `permissions:` pro Job (Least Privilege)
- Versionierung nach SemVer über Git-Tags (`v1`, `v1.0.0`)

## Lizenz

[MIT](LICENSE)
