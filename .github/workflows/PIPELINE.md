# CI/CD Pipeline-Dokumentation

Diese Dokumentation beschreibt die vollständige CI/CD-Pipeline für das AltDrag-Projekt.

## 📊 Pipeline-Übersicht

```
┌─────────────────────────────────────────────────────────────┐
│                     GitHub Repository                        │
└─────────────────┬───────────────────────────────────────────┘
                  │
    ┌─────────────┴─────────────┐
    │                           │
    ▼                           ▼
┌─────────┐                 ┌──────────┐
│  Push   │                 │   Tag    │
│   PR    │                 │  (v*.*)  │
└────┬────┘                 └─────┬────┘
     │                            │
     ├────────────────────────────┤
     │                            │
     ▼                            ▼
┌──────────────┐          ┌──────────────┐
│ Build & Test │          │   Release    │
│   Workflow   │          │   Workflow   │
└──────┬───────┘          └──────┬───────┘
       │                         │
       ▼                         ▼
┌──────────────┐          ┌──────────────┐
│  Artifacts   │          │   GitHub     │
│   Upload     │          │   Release    │
└──────────────┘          └──────────────┘
```

## 🔄 Workflows

### 1. Build Workflow (`build.yml`)

**Trigger:**
- Push auf `master` oder `cursor/**` Branches
- Pull Requests nach `master`
- Manuell über Workflow Dispatch

**Schritte:**
1. Repository auschecken
2. Dependencies installieren (MinGW-w64, NSIS)
3. Debug-Build kompilieren
4. Release-Build kompilieren
5. Build-Artefakte hochladen
6. Installer hochladen

**Artefakte:**
- `altdrag-build-{sha}`: Alle kompilierten Binärdateien
- `altdrag-installer-{sha}`: NSIS-Installer

**Dauer:** ~5-10 Minuten

### 2. Release Workflow (`release.yml`)

**Trigger:**
- Push von Tags (Format: `v*`)
- Manuell über Workflow Dispatch

**Schritte:**
1. Repository auschecken
2. Dependencies installieren
3. Release-Build kompilieren
4. GitHub Release erstellen
5. Artefakte zum Release hinzufügen

**Release-Inhalte:**
- AltDrag.exe (32-bit)
- hooks.dll (32-bit)
- HookWindows_x64.exe (64-bit)
- hooks_x64.dll (64-bit)
- AltDrag-Setup.exe (Installer)
- sha256sum.txt (Checksummen)

**Dauer:** ~5-10 Minuten

### 3. CodeQL Analysis (`codeql.yml`)

**Trigger:**
- Push auf `master`
- Pull Requests nach `master`
- Wöchentlich (Montags um Mitternacht)

**Schritte:**
1. Repository auschecken
2. CodeQL initialisieren
3. Code kompilieren
4. Sicherheitsanalyse durchführen
5. Ergebnisse hochladen

**Sprachen:** C/C++

**Dauer:** ~15-20 Minuten

### 4. PR Checks (`pr-checks.yml`)

**Trigger:**
- Pull Request opened/synchronized/reopened

**Schritte:**

#### Build Verification:
1. Debug-Build verifizieren
2. Release-Build verifizieren
3. Build-Ausgaben überprüfen
4. Checksummen verifizieren
5. Build-Zusammenfassung erstellen

#### File Changes:
1. Geänderte Dateien abrufen
2. Dateien auflisten
3. Kritische Dateien überprüfen

**Dauer:** ~5-10 Minuten

### 5. Stale Bot (`stale.yml`)

**Trigger:**
- Täglich um Mitternacht
- Manuell über Workflow Dispatch

**Funktion:**
- Markiert Issues/PRs als "stale" nach 60 Tagen Inaktivität
- Schließt sie nach weiteren 14 Tagen
- Ausnahmen für gelabelte Issues (pinned, security, enhancement)

## 🔐 Security

### CodeQL

CodeQL führt statische Sicherheitsanalysen durch:

- **Sicherheitslücken**: Pufferüberläufe, Use-after-free, etc.
- **Code-Qualität**: Ungenutzte Variablen, Memory Leaks
- **Best Practices**: Coding-Standard-Verstöße

Ergebnisse sind im Security-Tab verfügbar.

### Dependabot

Automatische Updates für:
- GitHub Actions Dependencies

Konfiguration in `.github/dependabot.yml`

## 📦 Artefakte

### Build-Artefakte

**Aufbewahrung:** 30 Tage

**Inhalt:**
```
bin/
├── AltDrag.exe
├── hooks.dll
├── HookWindows_x64.exe
├── hooks_x64.dll
└── sha256sum.txt
```

### Release-Artefakte

**Aufbewahrung:** Permanent (Teil des Releases)

**Download-URLs:**
```
https://github.com/USER/altdrag/releases/download/v1.1/AltDrag.exe
https://github.com/USER/altdrag/releases/download/v1.1/hooks.dll
https://github.com/USER/altdrag/releases/download/v1.1/HookWindows_x64.exe
https://github.com/USER/altdrag/releases/download/v1.1/hooks_x64.dll
https://github.com/USER/altdrag/releases/download/v1.1/AltDrag-Setup.exe
https://github.com/USER/altdrag/releases/download/v1.1/sha256sum.txt
```

## 🚀 Release-Prozess

### Automatisches Release (empfohlen)

```bash
# 1. Version im Code aktualisieren (falls nötig)
# 2. Änderungen committen
git add .
git commit -m "Prepare release v1.1.0"

# 3. Tag erstellen
git tag v1.1.0

# 4. Tag pushen (triggert Release-Workflow)
git push origin v1.1.0
```

### Manuelles Release

1. Gehen Sie zu Actions → Release
2. Klicken Sie auf "Run workflow"
3. Geben Sie den Tag-Namen ein (z.B. `v1.1.0`)
4. Klicken Sie auf "Run workflow"

### Release-Checklist

- [ ] Version im Code aktualisiert
- [ ] CHANGELOG.md aktualisiert (falls vorhanden)
- [ ] Alle Tests laufen durch
- [ ] Build läuft erfolgreich
- [ ] Tag erstellt und gepusht
- [ ] Release-Workflow erfolgreich
- [ ] Release-Notes überprüft
- [ ] Artefakte getestet

## 🔍 Monitoring & Debugging

### Workflow-Status anzeigen

```bash
# Alle Workflows auflisten
gh run list

# Workflow-Details anzeigen
gh run view [run-id]

# Workflow-Logs anzeigen
gh run view [run-id] --log

# Fehlgeschlagene Workflows
gh run list --status failure
```

### Häufige Probleme

#### Build schlägt fehl

```bash
# Lokale Reproduktion
./build.sh

# Überprüfen Sie:
# - Alle Quelldateien vorhanden?
# - Syntax-Fehler im Code?
# - Resource-Dateien korrekt?
```

#### Installer-Erstellung fehlgeschlagen

```bash
# Überprüfen Sie:
# - installer.nsi Syntax
# - Alle referenzierten Dateien vorhanden?
# - NSIS korrekt installiert?
```

#### CodeQL-Fehler

```bash
# CodeQL benötigt erfolgreichen Build
# Überprüfen Sie Build-Schritte in codeql.yml
```

## 📈 Metriken

### Build-Zeiten (Durchschnitt)

- Debug Build: ~2 Minuten
- Release Build: ~3 Minuten
- Installer: ~1 Minute
- CodeQL: ~15 Minuten
- Gesamt: ~5-10 Minuten

### Ressourcen

- **Runner:** ubuntu-latest (2 vCPUs, 7GB RAM)
- **Disk:** ~10GB verfügbar
- **Netzwerk:** High-speed GitHub Actions

## 🔄 Pipeline-Updates

### Workflow aktualisieren

```bash
# 1. Workflow-Datei bearbeiten
vim .github/workflows/build.yml

# 2. Änderungen testen (lokaler Act-Test, optional)
act push

# 3. Committen und pushen
git add .github/workflows/build.yml
git commit -m "Update build workflow"
git push
```

### Neue Schritte hinzufügen

Beispiel - Lint-Check hinzufügen:

```yaml
- name: Run Linter
  run: |
    # Installieren Sie Ihren Linter
    sudo apt-get install -y cppcheck
    
    # Linter ausführen
    cppcheck --enable=all --suppress=missingIncludeSystem *.c
```

## 📞 Support

Bei Problemen mit der Pipeline:

1. Überprüfen Sie die Workflow-Logs in GitHub Actions
2. Suchen Sie in den Issues nach ähnlichen Problemen
3. Erstellen Sie ein Issue mit dem Label "ci/cd"

---

**Letzte Aktualisierung:** 2025-12-23
**Version:** 1.0
**Maintainer:** AltDrag Team
