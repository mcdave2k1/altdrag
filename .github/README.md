# AltDrag CI/CD Pipeline

Willkommen zur CI/CD-Pipeline-Dokumentation für AltDrag!

## 📚 Dokumentations-Übersicht

- **[QUICKSTART.md](QUICKSTART.md)** - Schnellstart-Anleitung (START HIER! ⭐)
- **[PIPELINE_OVERVIEW.md](PIPELINE_OVERVIEW.md)** - Visuelle Übersicht mit Diagrammen
- **[workflows/PIPELINE.md](workflows/PIPELINE.md)** - Vollständige technische Dokumentation

## 🚀 Workflows

| Datei | Beschreibung | Trigger |
|-------|--------------|---------|
| [build.yml](workflows/build.yml) | Haupt-Build-Workflow | Push/PR |
| [release.yml](workflows/release.yml) | Release-Automatisierung | Tags (v*) |
| [codeql.yml](workflows/codeql.yml) | Sicherheitsanalyse | Wöchentlich |
| [pr-checks.yml](workflows/pr-checks.yml) | PR-Validierung | Pull Requests |
| [stale.yml](workflows/stale.yml) | Issue/PR Management | Täglich |

## 📝 Vorlagen

- **[ISSUE_TEMPLATE/bug_report.md](ISSUE_TEMPLATE/bug_report.md)** - Bug-Berichte
- **[ISSUE_TEMPLATE/feature_request.md](ISSUE_TEMPLATE/feature_request.md)** - Feature-Anfragen
- **[PULL_REQUEST_TEMPLATE.md](PULL_REQUEST_TEMPLATE.md)** - Pull Request-Vorlage

## ⚙️ Konfiguration

- **[dependabot.yml](dependabot.yml)** - Automatische Dependency-Updates

## 🎯 Schnellzugriff

### Für Entwickler
1. [Wie erstelle ich einen PR?](../CONTRIBUTING.md#pull-request-prozess)
2. [Lokales Testen](../CONTRIBUTING.md#build-anleitung)
3. [Coding Standards](../CONTRIBUTING.md#coding-standards)

### Für Maintainer
1. [Release erstellen](workflows/PIPELINE.md#release-prozess)
2. [Workflows überwachen](workflows/PIPELINE.md#monitoring--debugging)
3. [Pipeline aktualisieren](workflows/PIPELINE.md#pipeline-updates)

## 📊 Status

Aktuelle Pipeline-Version: **1.0**  
Letztes Update: **2025-12-23**  
Status: ✅ **Aktiv und produktionsbereit**

## 🆘 Hilfe

- **Fragen?** → [GitHub Discussions](https://github.com/stefansundin/altdrag/discussions)
- **Probleme?** → [GitHub Issues](https://github.com/stefansundin/altdrag/issues)
- **CI/CD Probleme?** → Label mit `ci/cd`

---

**Tipp**: Starten Sie mit [QUICKSTART.md](QUICKSTART.md) für eine schnelle Einführung! 🚀
