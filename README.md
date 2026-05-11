# MD-Viewer

**Aktuelle Version: v26.2.1**

Single-File Markdown-Betrachter und -Editor mit Drag-&-Drop-Schnittstelle, Live-Editor mit synchronem Scroll, zweisprachiger Oberfläche, HTML→Markdown-Konvertierung beim Einfügen und mehreren Design-Varianten. Vollständig offline-fähig nach erstem Laden, ohne Build-Schritt, ohne Server, ohne Telemetrie.

---

## Konzeption

Die Anwendung folgt dem Vorbild des [edge-md-viewer](https://github.com/0xedgelessblade/edge-md-viewer) (Single HTML, zero Build, offline-fähig) und ergänzt diesen um eine zentrale Drop-Fläche im Stil typischer GAEB-Viewer, ein erweitertes Themen-System, bidirektionale Editor-Vorschau-Synchronisation sowie eine automatische Erkennung von Tabellen und anderen Strukturen beim Einfügen aus Webseiten.

## Funktionsumfang

- **Drag & Drop** beliebiger Markdown-Dateien (`.md`, `.markdown`, `.mdown`, `.mkd`, `.txt`) — sowohl auf die zentrale Dropzone als auch global über das Browserfenster
- **Neu-Button** (Strg/Cmd+N) zur Erstellung leerer Markdown-Dokumente; das erste Speichern öffnet einen Speicherdialog
- **HTML→Markdown-Konvertierung beim Einfügen** — Inhalt aus Webseiten (Tabellen, Listen, Überschriften, Hyperlinks, Fettungen, Code-Blöcke) wird beim Paste automatisch in GitHub-Flavored-Markdown übersetzt; Plain-Text bleibt unverändert
- **Acht Design-Varianten** mit Persistierung im `localStorage`:
  - *Hell – Stone* (warmes Beige, Source Serif)
  - *Dunkel – Onyx* (Anthrazit-Dunkelmodus)
  - *Sepia – Pergament* (papierähnlicher Leseton)
  - *Akademisch – Paper* (Journal-Layout, Computer-Modern-Anmutung)
  - *Solarized* (etablierte Entwickler-Palette)
  - *Nord – Polar* (kühles Blau)
  - *Terminal – Mono* (Konsolen-Optik)
  - *Hochkontrast* (Barrierefreiheit, WCAG-orientiert)
- **Sprachumschaltung** Deutsch/Englisch über SVG-Flaggen-Buttons in der Toolbar
- **Info-Button** lädt eine zweisprachige Funktionsübersicht als Demo-Dokument
- **Live-Editor** (Strg+E) mit synchroner Vorschau (250 ms Debounce)
- **Bidirektionaler Scroll-Sync** zwischen Editor und Vorschau (proportional)
- **Speicherung** zurück in die Originaldatei via [File System Access API](https://developer.mozilla.org/en-US/docs/Web/API/File_System_Access_API), mit Download-Fallback in nicht unterstützenden Browsern
- **HTML-Export** als eigenständiges Dokument mit eingebettetem CSS
- **Mathematik-Rendering** über KaTeX (`$…$` inline, `$$…$$` Block)
- **Code-Syntaxhervorhebung** über highlight.js
- **Statusleiste** mit Dateiname, Dirty-State-Anzeige für ungespeicherte Dateien, aktuellem Datum, Versionsnummer und Autorenlink
- **Druckansicht** mit automatisch ausgeblendeter Toolbar und Statusleiste

## Tastenkürzel

| Kürzel       | Funktion                          |
|--------------|-----------------------------------|
| `Strg/Cmd+O` | Datei öffnen                      |
| `Strg/Cmd+N` | Neue Datei anlegen                |
| `Strg/Cmd+S` | Speichern                         |
| `Strg/Cmd+E` | Editor öffnen/schließen           |
| `Esc`        | Editor schließen                  |

## Versionierungsschema

Die Versionsnummer folgt dem Format `Jahr.Push.Iteration`:

| Komponente    | Bedeutung                                                          |
|---------------|--------------------------------------------------------------------|
| **Jahr**      | Zweistellige Jahreszahl (aktuell `26` für 2026)                    |
| **Push**      | Fortlaufende Nummer der GitHub-Pushes innerhalb des Kalenderjahres |
| **Iteration** | Kleinere Änderungen zwischen zwei Pushes (auch lokal)              |

Bei jedem GitHub-Push wird die Push-Zahl inkrementiert, die Iteration auf `1` zurückgesetzt und sämtliche Dokumentation (`README.md`, `CHANGELOG.md`, der eingebaute Info-Text) auf den aktuellen Funktionsstand gebracht.

Die Versionsnummer wird an drei Stellen geführt und muss bei Änderungen konsistent aktualisiert werden:

1. JavaScript-Konstante `APP_VERSION` in `md-viewer.html`
2. Header der `CHANGELOG.md` (neuer Eintrag)
3. Header dieser `README.md`

## Technische Architektur

Eine einzelne HTML-Datei ohne Build-Schritt. Folgende externe Bibliotheken werden über `cdn.jsdelivr.net` nachgeladen:

| Bibliothek            | Version  | Zweck                          |
|-----------------------|----------|--------------------------------|
| marked.js             | 12.0.2   | Markdown-Parser (GFM)          |
| DOMPurify             | 3.0.11   | XSS-Sanitizer                  |
| highlight.js          | 11.9.0   | Code-Syntax-Highlighting       |
| KaTeX                 | 0.16.10  | Mathematik-Rendering           |
| turndown              | 7.2.0    | HTML→Markdown beim Paste       |
| turndown-plugin-gfm   | 1.0.2    | GFM-Tabellen für Turndown      |

Sämtliche Verarbeitung erfolgt clientseitig; keine Daten werden an externe Server übertragen.

## Inbetriebnahme

### Lokal

Die Datei `md-viewer.html` kann direkt im Browser geöffnet werden — etwa per Doppelklick im Finder oder via `open md-viewer.html` im Terminal. Für die volle Funktionalität der File-System-Access-API ist ein chromiumbasierter Browser erforderlich (Chrome, Edge, Brave, Arc); in Firefox und Safari greift der Download-Fallback.

### Als GitHub Pages

Das Repository kann unmittelbar als GitHub Pages bereitgestellt werden. Die `index.html` leitet automatisch auf `md-viewer.html` weiter. Der mitgelieferte Workflow unter `.github/workflows/pages.yml` deployt bei jedem Push auf den `main`-Branch.

Aktivierung in den Repository-Einstellungen: *Settings → Pages → Source: GitHub Actions*.

## Projektstruktur

```
md-viewer-editor/
├── md-viewer.html               Hauptanwendung (Single-File)
├── index.html                   Weiterleitung für GitHub Pages
├── README.md                    Diese Datei
├── CHANGELOG.md                 Versionshistorie
├── CONTRIBUTING.md              Release-Prozess & Versionierungsregeln
├── LICENSE                      MIT-Lizenz
├── .gitignore                   Auszuschließende Dateien
├── .github/
│   └── workflows/
│       └── pages.yml            GitHub-Pages-Deploy-Workflow
└── examples/
    └── sample.md                Beispieldokument zum Testen
```

## Bekannte Einschränkungen

- Die *File System Access API* steht in Firefox und Safari aktuell nicht zur Verfügung; Speicherung erfolgt dort über Download-Dialog.
- Externe Bibliotheken werden aus dem CDN nachgeladen; ein erster Aufruf erfordert Netzwerkzugriff. Anschließend können sie aus dem Browser-Cache offline bedient werden.
- Bei restriktiven Content-Security-Policies oder Adblockern, die `cdn.jsdelivr.net` blockieren, erscheint nach ca. 10 Sekunden eine sprechende Fehlermeldung.

## Mitwirkende

Konzept und Umsetzung: [Michael Radeck](https://www.michael-radeck.de)

## Lizenz

MIT – siehe [`LICENSE`](./LICENSE).
