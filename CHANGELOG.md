# Changelog

Sämtliche relevanten Änderungen an diesem Projekt werden in dieser Datei dokumentiert.

Das Format orientiert sich an [Keep a Changelog](https://keepachangelog.com/de/1.1.0/).
Das Projekt folgt einer eigenen Versionierung im Format `Jahr.Push.Iteration` (siehe [`README.md`](./README.md)).

---

## [26.3.1] – 2026-05-11

Dritter GitHub-Push.

### Hinzugefügt
- **Titel als Dateinamen-Vorschlag**: Beim erstmaligen Speichern eines neu angelegten Dokuments wird die erste Markdown-H1-Überschrift extrahiert, von Formatierung und filesystem-unsicheren Zeichen bereinigt und als Vorschlag in den Speicherdialog (`showSaveFilePicker`) eingesetzt. Ist die Überschrift unverändert (`Neues Dokument` / `New document`), bleibt der Fallback `unbenannt.md` / `untitled.md` erhalten.
- Neue Helper-Funktion `deriveFilenameFromContent(text)` zur Titel-Extraktion: behandelt Markdown-Links (`[Text](url)` → Text), entfernt Emphasis-Marker (`*`, `_`, `` ` ``, `~`), ersetzt filesystem-unsichere Zeichen (`/ \ : * ? " < > |`) durch `-`, verdichtet Whitespace und begrenzt die Länge auf 100 Zeichen.

### Geändert
- `saveFile()` greift bei fehlendem `FileHandle` auf den abgeleiteten Titel zurück; der Speicherort bleibt im Dialog frei wählbar, der Dateiname kann dort weiterhin überschrieben werden.
- Eingebauter Info-Text (DE/EN) erwähnt die neue Titel-zu-Dateiname-Logik.

### Vorgehen
- Build erfolgte über chirurgische Eingriffe via Python-Update-Skript, ausgeführt per `osascript` direkt auf dem Mac-Filesystem — kein vollständiges Überschreiben der HTML-Datei.

---

## [26.2.1] – 2026-05-11

Zweiter GitHub-Push. Konsolidiert die lokalen Iterationen seit `26.1.1`.

### Hinzugefügt
- **„Neu"/„New"-Button** rechts neben „Öffnen" zur Erstellung leerer Markdown-Dokumente
- Tastenkürzel `Strg/Cmd + N` für neue Dateien
- Automatisches Öffnen des Editors beim Anlegen eines neuen Dokuments mit vorbereitetem Template
- Dirty-State-Anzeige in der Fußzeile (`unbenannt.md · ungespeichert` in Akzentfarbe) für ungespeicherte neue Dateien
- **HTML→Markdown-Konvertierung beim Einfügen**: Aus Webseiten oder anderen HTML-Quellen kopierte Inhalte (Tabellen, Listen, Überschriften, Hyperlinks, Fettungen, Code-Blöcke) werden automatisch in GitHub-Flavored-Markdown übersetzt
- Integration von `turndown@7.2.0` und `turndown-plugin-gfm@1.0.2` als CDN-Bibliotheken
- Toast-Benachrichtigung „HTML als Markdown eingefügt" / „HTML inserted as Markdown" beim erfolgreichen Paste-Conversion-Vorgang

### Geändert
- `saveFile()` nutzt `showSaveFilePicker` als Erstspeicher-Dialog, sobald kein FileHandle vorhanden ist (typisch bei „Neu" oder Info-Dokument)
- Drop-Zone-Hinweis erweitert um `Strg+N` für neue Dateien
- Eingebauter Info-Text und README durchgängig auf den neuen Funktionsstand aktualisiert

### Technisch
- Plain-Text-Paste verbleibt unverändert (Heuristik prüft auf strukturelle HTML-Tags vor Konvertierung)
- Fehlertolerante Implementierung: scheitert die HTML→MD-Konvertierung, fällt das Verhalten automatisch auf den Standard-Paste des Browsers zurück

---

## [26.1.1] – 2026-05-11

Initiale Veröffentlichung mit vollständigem Funktionsumfang.

### Hinzugefügt
- Single-File Markdown-Viewer mit `marked.js` und `DOMPurify`
- Zentrale Drag-&-Drop-Fläche im Stil von GAEB-Viewern
- Globales Drop-Overlay über das gesamte Browserfenster
- Acht Design-Varianten: Hell, Dunkel, Sepia, Akademisch, Solarized, Nord, Terminal, Hochkontrast
- Persistierung von Themen- und Sprachwahl im `localStorage`
- Live-Editor mit 250 ms Debounce zur Vorschau
- Bidirektionaler synchroner Scroll zwischen Editor und Vorschau (proportional)
- Sprachumschaltung Deutsch/Englisch über SVG-Flaggen
- Info-Button mit zweisprachiger Funktionsübersicht als Demo-Dokument
- File System Access API zum direkten Speichern in die Originaldatei
- Download-Fallback für Firefox und Safari
- HTML-Export als eigenständiges Dokument mit eingebettetem CSS
- KaTeX-Integration für mathematische Notation (inline und Block)
- highlight.js für Code-Syntax-Highlighting
- Tastenkürzel `Cmd/Ctrl + O/S/E` und `Esc`
- Statusleiste am unteren Bildschirmrand mit Dateiname, Datum, Versionsnummer und Autorenlink
- Druckansicht mit automatisch ausgeblendeten UI-Elementen
- GitHub-Pages-Workflow zur automatischen Bereitstellung

### Geändert
- Default-Startzustand zeigt die Drop-Fläche statt eines vorab geladenen Demo-Dokuments; der Funktionsüberblick lässt sich über den Info-Button explizit aufrufen
- Der Dateiname wird ausschließlich in der Fußzeile angezeigt, nicht mehr in der Toolbar

### Technisch
- CDN-Wechsel von `cdnjs.cloudflare.com` auf `cdn.jsdelivr.net` zur robusteren Verfügbarkeit in restriktiven Netzwerkumgebungen
- Entfernung der SRI-Integrity-Attribute, da abweichende Hashes ein vollständiges Blockieren des Skripts durch den Browser auslösen
- Wartelogik (`waitForLibraries`) verhindert `marked is not defined`, falls externe Skripte verzögert eintreffen

---

## Erwartete Folgeversionen

- **26.4.x** — nächster GitHub-Push
- **27.x.x** — Versionssprung mit Jahreswechsel
