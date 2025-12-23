# AltDrag

[![Build](https://github.com/stefansundin/altdrag/actions/workflows/build.yml/badge.svg)](https://github.com/stefansundin/altdrag/actions/workflows/build.yml)
[![Release](https://github.com/stefansundin/altdrag/actions/workflows/release.yml/badge.svg)](https://github.com/stefansundin/altdrag/actions/workflows/release.yml)
[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](LICENSE)

AltDrag ist ein Windows-Programm, das es ermöglicht, Fenster zu verschieben und deren Größe zu ändern, indem man die Alt-Taste gedrückt hält und dann mit der Maus klickt und zieht.

## 🚀 Features

- Verschieben von Fenstern durch Klicken und Ziehen mit Alt-Taste
- Größenänderung von Fenstern mit Alt + Rechtsklick
- Anpassbare Hotkeys und Einstellungen
- Unterstützung für mehrere Sprachen
- Portable und Installer-Version verfügbar

## 📦 Download

Die neueste Version kann von der [Releases-Seite](https://github.com/stefansundin/altdrag/releases) heruntergeladen werden.

### Versionen

- **Installer** (empfohlen): `AltDrag-Setup.exe`
- **Portable 32-bit**: `AltDrag.exe` + `hooks.dll`
- **Portable 64-bit**: `HookWindows_x64.exe` + `hooks_x64.dll`

## 🔨 Build-Anleitung

### Voraussetzungen

#### Linux (Ubuntu/Debian)
```bash
sudo apt-get install gcc-mingw-w64 nsis
```

#### Windows
- MinGW-w64 ([Download](https://www.mingw-w64.org/))
- NSIS ([Download](https://nsis.sourceforge.io/))

### Kompilieren

#### Debug-Build (Entwicklung)
```bash
# Linux
./build.sh

# Windows
build.bat
```

#### Release-Build (mit Installer)
```bash
# Linux
./build.sh release

# Windows
build.bat all x64
```

Die kompilierten Dateien befinden sich im `bin/` Verzeichnis.

## 🤖 CI/CD Pipeline

Das Projekt verwendet GitHub Actions für automatische Builds und Releases. Für detaillierte Informationen siehe:
- **[Pipeline-Übersicht](.github/PIPELINE_OVERVIEW.md)** - Visuelle Darstellung
- **[Pipeline-Dokumentation](.github/workflows/PIPELINE.md)** - Technische Details

### Build Workflow
- **Trigger**: Push auf `master` oder `cursor/**` Branches, Pull Requests
- **Actions**: 
  - Installiert Dependencies (MinGW-w64, NSIS)
  - Kompiliert Debug- und Release-Versionen
  - Lädt Build-Artefakte hoch
  - Erstellt Installer

### Release Workflow
- **Trigger**: Push von Tags (z.B. `v1.1.0`) oder manuell
- **Actions**:
  - Kompiliert Release-Version
  - Erstellt GitHub Release mit allen Binärdateien
  - Generiert SHA256-Checksummen

### Weitere Workflows
- **CodeQL**: Automatische Sicherheitsanalyse (wöchentlich)
- **PR-Checks**: Zusätzliche Validierung für Pull Requests
- **Stale Bot**: Verwaltung inaktiver Issues/PRs
- **Dependabot**: Automatische Dependency-Updates

### Manuelles Release erstellen

```bash
# Tag erstellen und pushen
git tag v1.1.0
git push origin v1.1.0

# Oder über GitHub Actions manuell auslösen
# (Workflow Dispatch im Actions-Tab)
```

## 🌐 Lokalisierung

AltDrag unterstützt mehrere Sprachen. Übersetzungsdateien befinden sich im `localization/` Verzeichnis:

- Katalanisch (ca_ES)
- Deutsch (de_DE)
- Englisch (en_US)
- Spanisch (es_ES)
- Französisch (fr_FR)
- Galizisch (gl_ES)
- Italienisch (it_IT)
- Japanisch (ja_JP)
- Koreanisch (ko_KR)
- Norwegisch (nb_NO)
- Niederländisch (nl_NL)
- Polnisch (pl_PL)
- Portugiesisch (pt_BR)
- Russisch (ru_RU)
- Slowakisch (sk_SK)
- Chinesisch (zh_CN, zh_TW)

## 📋 Projektstruktur

```
altdrag/
├── .github/
│   └── workflows/       # GitHub Actions Workflows
├── config/              # Konfigurations-Dateien
├── include/             # Header- und Ressourcen-Dateien
├── localization/        # Übersetzungsdateien
├── media/               # Icons und Cursor
├── tools/               # Build-Tools
├── altdrag.c            # Hauptprogramm
├── hooks.c              # Hook-Bibliothek
├── hookwindows_x64.c    # 64-bit Hook-Programm
├── build.sh             # Linux Build-Skript
├── build.bat            # Windows Build-Skript
└── installer.nsi        # NSIS Installer-Skript
```

## 📄 Lizenz

Dieses Projekt ist unter der GNU General Public License v3.0 lizenziert. Siehe [LICENSE](LICENSE) für Details.

## 🔗 Links

- **Website**: [https://stefansundin.github.io/altdrag/](https://stefansundin.github.io/altdrag/)
- **GitHub**: [https://github.com/stefansundin/altdrag](https://github.com/stefansundin/altdrag)

## 🤝 Beiträge

Beiträge sind willkommen! Bitte erstellen Sie einen Pull Request mit Ihren Änderungen.

1. Fork das Repository
2. Erstellen Sie einen Feature-Branch (`git checkout -b feature/NeuesFeature`)
3. Committen Sie Ihre Änderungen (`git commit -am 'Füge neues Feature hinzu'`)
4. Pushen Sie den Branch (`git push origin feature/NeuesFeature`)
5. Öffnen Sie einen Pull Request

Die CI-Pipeline wird automatisch Ihren Code kompilieren und testen.

---

Made with ❤️ by Stefan Sundin and contributors
