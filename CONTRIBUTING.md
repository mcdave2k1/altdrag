# Beitragen zu AltDrag

Vielen Dank für Ihr Interesse, zu AltDrag beizutragen! Dieses Dokument enthält Richtlinien und Anweisungen für Beiträge.

## 📋 Inhaltsverzeichnis

- [Code of Conduct](#code-of-conduct)
- [Erste Schritte](#erste-schritte)
- [Entwicklungsumgebung einrichten](#entwicklungsumgebung-einrichten)
- [Wie Sie beitragen können](#wie-sie-beitragen-können)
- [Pull Request Prozess](#pull-request-prozess)
- [Coding Standards](#coding-standards)
- [Build-Anleitung](#build-anleitung)
- [CI/CD Pipeline](#cicd-pipeline)

## Code of Conduct

Durch Ihre Teilnahme an diesem Projekt stimmen Sie zu, respektvoll und professionell zu handeln. Wir erwarten:

- Respektvolle und konstruktive Kommunikation
- Fokus auf das, was für die Community am besten ist
- Empathie gegenüber anderen Community-Mitgliedern

## Erste Schritte

1. **Fork** das Repository
2. **Clone** Ihren Fork lokal
3. **Erstellen** Sie einen neuen Branch für Ihre Änderungen
4. **Machen** Sie Ihre Änderungen
5. **Testen** Sie Ihre Änderungen gründlich
6. **Committen** Sie Ihre Änderungen mit aussagekräftigen Commit-Messages
7. **Push** zu Ihrem Fork
8. **Erstellen** Sie einen Pull Request

## Entwicklungsumgebung einrichten

### Windows

1. Installieren Sie [MinGW-w64](https://www.mingw-w64.org/)
2. Installieren Sie [NSIS](https://nsis.sourceforge.io/)
3. Fügen Sie MinGW-w64 und NSIS zu Ihrem PATH hinzu

```cmd
git clone https://github.com/DEIN_USERNAME/altdrag.git
cd altdrag
build.bat
```

### Linux

```bash
sudo apt-get install gcc-mingw-w64 nsis
git clone https://github.com/DEIN_USERNAME/altdrag.git
cd altdrag
chmod +x build.sh
./build.sh
```

## Wie Sie beitragen können

### 🐛 Bugs melden

Wenn Sie einen Bug finden:

1. Überprüfen Sie, ob das Problem bereits gemeldet wurde
2. Wenn nicht, erstellen Sie ein neues Issue mit unserem Bug-Report-Template
3. Geben Sie so viele Details wie möglich an:
   - Betriebssystem und Version
   - AltDrag Version
   - Schritte zur Reproduktion
   - Erwartetes vs. tatsächliches Verhalten

### 💡 Features vorschlagen

Für Feature-Vorschläge:

1. Überprüfen Sie, ob das Feature bereits vorgeschlagen wurde
2. Erstellen Sie ein Issue mit unserem Feature-Request-Template
3. Beschreiben Sie:
   - Das Problem, das Sie lösen möchten
   - Ihre vorgeschlagene Lösung
   - Warum dies für andere Nutzer wertvoll wäre

### 🔧 Code beitragen

1. Wählen Sie ein Issue aus oder erstellen Sie eines
2. Kommentieren Sie, dass Sie daran arbeiten möchten
3. Fork und erstellen Sie einen Branch
4. Implementieren Sie Ihre Änderungen
5. Testen Sie gründlich
6. Erstellen Sie einen Pull Request

### 🌐 Übersetzungen

Wir freuen uns über Übersetzungen in weitere Sprachen!

1. Kopieren Sie den `localization/en_US/` Ordner
2. Benennen Sie ihn nach dem Sprachcode (z.B. `de_DE`)
3. Übersetzen Sie die Strings in `strings.h` und `Translation.ini`
4. Erstellen Sie einen Pull Request

## Pull Request Prozess

### Vor dem Erstellen eines PRs

- [ ] Stellen Sie sicher, dass Ihr Code kompiliert
- [ ] Testen Sie Ihre Änderungen auf Windows (32-bit und 64-bit wenn möglich)
- [ ] Überprüfen Sie, dass keine neuen Warnungen generiert werden
- [ ] Aktualisieren Sie die Dokumentation falls nötig
- [ ] Schreiben Sie einen aussagekräftigen PR-Titel und Beschreibung

### CI/CD Checks

Ihr Pull Request wird automatisch durch unsere CI/CD-Pipeline überprüft:

1. **Build Check**: Kompiliert Debug- und Release-Versionen
2. **CodeQL Analysis**: Statische Code-Analyse für Sicherheit
3. **File Changes**: Überprüft geänderte Dateien
4. **Checksum Verification**: Verifiziert Build-Integrität

Alle Checks müssen erfolgreich sein, bevor ein PR gemerged werden kann.

### Review-Prozess

1. Mindestens ein Maintainer wird Ihren PR reviewen
2. Änderungen können angefordert werden
3. Nach Genehmigung wird der PR gemerged
4. Ihr Beitrag wird im nächsten Release enthalten sein

## Coding Standards

### C Code Style

```c
// Verwenden Sie aussagekräftige Variablennamen
int window_height = 100;  // Gut
int wh = 100;             // Schlecht

// Kommentieren Sie komplexe Logik
// Check if window is visible and not minimized
if (IsWindowVisible(hwnd) && !IsIconic(hwnd)) {
    // ...
}

// Verwenden Sie konsistente Einrückung (Spaces oder Tabs)
// Folgen Sie dem vorhandenen Stil im Projekt
```

### Commit Messages

Verwenden Sie aussagekräftige Commit-Messages:

```
Gut:
- "Fix: Window resize not working on Windows 11"
- "Add: Support for custom hotkey combinations"
- "Update: German translation strings"

Schlecht:
- "fix bug"
- "update"
- "changes"
```

### Branch-Naming

```
feature/neue-funktion-name
bugfix/issue-nummer-kurze-beschreibung
docs/dokumentation-update
translation/sprach-code
```

## Build-Anleitung

### Debug Build (Entwicklung)

```bash
# Linux
./build.sh

# Windows
build.bat
```

Debug-Builds enthalten:
- Debug-Symbole für Debugging
- Keine Optimierung
- DEBUG-Flag aktiviert

### Release Build

```bash
# Linux
./build.sh release

# Windows
build.bat all x64
```

Release-Builds enthalten:
- Vollständige Optimierung
- Stripped binaries (kleinere Dateigröße)
- Installer (NSIS)
- SHA256-Checksummen

### Build-Ausgabe

```
bin/
├── AltDrag.exe          # 32-bit Hauptprogramm
├── hooks.dll            # 32-bit Hooks-Bibliothek
├── HookWindows_x64.exe  # 64-bit Helper-Programm
├── hooks_x64.dll        # 64-bit Hooks-Bibliothek
└── sha256sum.txt        # Checksummen-Datei
```

## CI/CD Pipeline

Unser Projekt verwendet GitHub Actions für automatisierte Tests und Deployments:

### Workflows

1. **build.yml**: Kompiliert bei jedem Push/PR
2. **release.yml**: Erstellt Releases bei Tags
3. **codeql.yml**: Wöchentliche Sicherheitsanalyse
4. **pr-checks.yml**: Zusätzliche Checks für Pull Requests
5. **stale.yml**: Markiert inaktive Issues/PRs

### Lokale Tests vor dem Push

Führen Sie diese Befehle aus, um sicherzustellen, dass CI erfolgreich sein wird:

```bash
# Cleanup
rm -rf bin/

# Debug Build testen
./build.sh

# Release Build testen
./build.sh release

# Checksummen verifizieren
cd bin && sha256sum -c sha256sum.txt
```

## Hilfe bekommen

Wenn Sie Fragen haben:

1. Überprüfen Sie die vorhandene Dokumentation
2. Suchen Sie in den Issues nach ähnlichen Fragen
3. Erstellen Sie ein neues Issue mit dem Label "question"
4. Seien Sie geduldig - dies ist ein Community-Projekt

## Lizenz

Durch das Beitragen zu AltDrag stimmen Sie zu, dass Ihre Beiträge unter der GPL v3 Lizenz lizenziert werden.

---

Vielen Dank, dass Sie AltDrag besser machen! 🎉
