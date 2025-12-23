# 🚀 CI/CD Pipeline - Schnellstart

Diese Anleitung hilft Ihnen, schnell mit der CI/CD-Pipeline zu starten.

## ✨ Was wurde eingerichtet?

Die vollständige CI/CD-Pipeline umfasst:

- ✅ **Automatische Builds** bei jedem Commit
- ✅ **Release-Automatisierung** bei Tags
- ✅ **Sicherheitsscans** (CodeQL)
- ✅ **Pull Request Validierung**
- ✅ **Issue/PR Management**
- ✅ **Dependency Updates** (Dependabot)

## 📁 Dateistruktur

```
.github/
├── workflows/
│   ├── build.yml          # ⚙️ Haupt-Build
│   ├── release.yml        # 📦 Release-Erstellung
│   ├── codeql.yml         # 🔐 Sicherheit
│   ├── pr-checks.yml      # ✓ PR-Validierung
│   └── stale.yml          # 🗑️ Cleanup
├── ISSUE_TEMPLATE/        # 📝 Issue-Vorlagen
├── PULL_REQUEST_TEMPLATE.md
├── dependabot.yml         # 🤖 Auto-Updates
├── PIPELINE.md            # 📚 Vollständige Doku
└── PIPELINE_OVERVIEW.md   # 📊 Übersicht

Zusätzlich:
- README.md               # ✨ Projekt-README
- CONTRIBUTING.md         # 🤝 Beitragsrichtlinien
```

## 🎯 Erste Schritte

### 1️⃣ Push-Code um Build zu testen

```bash
# Änderungen machen
echo "// Test" >> altdrag.c

# Committen und pushen
git add .
git commit -m "Test: CI/CD Pipeline"
git push origin cursor/build-pipeline-development-56a2
```

**Ergebnis**: Build-Workflow startet automatisch ✨

### 2️⃣ Pull Request erstellen

```bash
# Über GitHub UI oder CLI
gh pr create --title "Test PR" --body "Testing CI/CD"
```

**Ergebnis**: Alle PR-Checks werden ausgeführt ✅

### 3️⃣ Release erstellen

```bash
# Tag erstellen
git tag v1.1.0

# Tag pushen
git push origin v1.1.0
```

**Ergebnis**: Automatisches Release mit Binärdateien 📦

## 📊 Status überprüfen

### Im Browser

1. Gehen Sie zu: `https://github.com/USERNAME/altdrag/actions`
2. Sehen Sie alle laufenden/abgeschlossenen Workflows

### Via CLI

```bash
# Alle Workflows anzeigen
gh run list

# Neuesten Workflow-Status
gh run list --limit 1

# Workflow-Details
gh run view [run-id]

# Logs anzeigen
gh run view [run-id] --log
```

## 🔧 Workflow-Aktivierung

Die Workflows sind **sofort aktiv** nach dem Push!

### Verifizierung:

```bash
# 1. Workflow-Dateien überprüfen
ls -la .github/workflows/

# 2. Syntax validieren (lokal, optional)
# Installieren Sie 'actionlint' für lokale Validierung
# brew install actionlint (macOS)
# oder: https://github.com/rhysd/actionlint

actionlint .github/workflows/*.yml
```

## 🎨 Badge zu README hinzufügen

Die Build-Badges sind bereits in der README.md:

```markdown
[![Build](https://github.com/USERNAME/altdrag/actions/workflows/build.yml/badge.svg)](https://github.com/USERNAME/altdrag/actions/workflows/build.yml)
```

**Hinweis**: Ersetzen Sie `USERNAME` mit Ihrem GitHub-Benutzernamen!

## 🔐 Secrets konfigurieren (optional)

Für erweiterte Features:

```bash
# GitHub Token wird automatisch bereitgestellt
# Keine zusätzlichen Secrets erforderlich!

# Falls Sie eigene Secrets benötigen:
gh secret set MY_SECRET --body "secret-value"
```

## 📦 Artifacts herunterladen

### Nach einem Build:

```bash
# Neuestes Artifact auflisten
gh run list --limit 1

# Artifact herunterladen
gh run download [run-id]
```

### Von einem Release:

```bash
# Neuestes Release
gh release view

# Release herunterladen
gh release download v1.1.0
```

## 🐛 Troubleshooting

### Build schlägt fehl?

```bash
# 1. Lokal testen
./build.sh

# 2. Logs überprüfen
gh run view --log

# 3. Issue erstellen (wenn nötig)
gh issue create --title "CI: Build failed" --label "ci/cd"
```

### Workflow wird nicht ausgeführt?

```bash
# 1. Branch überprüfen
git branch --show-current

# 2. Workflow-Trigger überprüfen
cat .github/workflows/build.yml | grep "on:" -A 5

# 3. Permissions überprüfen
ls -la .github/workflows/
```

## 📚 Weiterführende Dokumentation

- **[PIPELINE.md](.github/workflows/PIPELINE.md)** - Vollständige technische Dokumentation
- **[PIPELINE_OVERVIEW.md](.github/PIPELINE_OVERVIEW.md)** - Visuelle Übersicht
- **[CONTRIBUTING.md](../CONTRIBUTING.md)** - Beitragsrichtlinien

## ✅ Checkliste: Pipeline ist bereit!

- [x] Workflows erstellt (5 Dateien)
- [x] Issue/PR-Vorlagen erstellt
- [x] Dependabot konfiguriert
- [x] Dokumentation erstellt
- [x] README aktualisiert
- [ ] **Nächster Schritt**: Pushen und testen!

## 🎉 Los geht's!

```bash
# Alles committen
git add .github/ README.md CONTRIBUTING.md
git commit -m "feat: Add CI/CD pipeline"

# Pushen und Pipeline aktivieren
git push origin $(git branch --show-current)

# Status beobachten
gh run watch
```

## 💡 Tipps

1. **Parallele Builds**: Workflows laufen parallel für schnellere Ergebnisse
2. **Caching**: Dependencies werden gecacht für schnellere Builds
3. **Artifacts**: Werden 30 Tage aufbewahrt
4. **Releases**: Bleiben permanent verfügbar
5. **Security**: CodeQL läuft automatisch wöchentlich

## 📞 Hilfe benötigt?

- **Dokumentation**: Siehe [PIPELINE.md](workflows/PIPELINE.md)
- **Issues**: [GitHub Issues](https://github.com/stefansundin/altdrag/issues)
- **Community**: [GitHub Discussions](https://github.com/stefansundin/altdrag/discussions)

---

**Pipeline-Version**: 1.0  
**Erstellt**: 2025-12-23  
**Status**: ✅ Bereit zur Nutzung!

Viel Erfolg mit Ihrer neuen CI/CD-Pipeline! 🚀
