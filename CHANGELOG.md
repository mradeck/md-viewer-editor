# Changelog

Sämtliche relevanten Änderungen an diesem Projekt werden in dieser Datei dokumentiert.

Das Format orientiert sich an [Keep a Changelog](https://keepachangelog.com/de/1.1.0/).
Das Projekt folgt einer eigenen Versionierung im Format `Jahr.Push.Iteration` (siehe [`README.md`](./README.md)).

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

- **26.2.x** — geplante nächste Push-Runde (Themen, Funktionserweiterungen, Bugfixes)
- **27.x.x** — Versionssprung mit Jahreswechsel
