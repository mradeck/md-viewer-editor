# Beiträge & Release-Prozess

## Versionierung

Die Versionsnummer folgt dem Format `Jahr.Push.Iteration`:

- **Jahr** – zweistellige Jahreszahl (z. B. `26` für 2026)
- **Push** – fortlaufende Nummer der GitHub-Pushes innerhalb des Kalenderjahres
- **Iteration** – kleinere Änderungen zwischen zwei Pushes (auch lokal)

Beispiele:

| Version | Bedeutung                                                       |
|---------|-----------------------------------------------------------------|
| 26.1.1  | 2026, erster Push, erste Iteration (Initialveröffentlichung)    |
| 26.1.2  | 2026, erster Push, zweite Iteration (lokale Korrektur)          |
| 26.2.1  | 2026, zweiter Push                                              |
| 27.1.1  | 2027, erster Push                                               |

## Release-Checkliste

Vor jedem `git push origin main` sind die folgenden Schritte abzuarbeiten, damit Versionierung und Dokumentation konsistent bleiben:

1. **Versionsnummer hochzählen**
   - In `md-viewer.html` die JavaScript-Konstante `APP_VERSION` aktualisieren
   - Push-Counter inkrementieren, Iteration auf `1` zurücksetzen

2. **`CHANGELOG.md` ergänzen**
   - Neuer Abschnitt mit der neuen Versionsnummer und dem aktuellen Datum (ISO-Format `YYYY-MM-DD`)
   - Auflistung in den Kategorien *Hinzugefügt*, *Geändert*, *Behoben*, *Entfernt*, *Technisch*

3. **`README.md` prüfen**
   - Versionsanzeige im Header aktualisieren
   - Funktionsumfang spiegelt den tatsächlichen Stand wider
   - Projektstruktur stimmt mit dem Repository überein

4. **Eingebaute Info-Texte aktualisieren**
   - In `md-viewer.html` das Demo-Markdown (`i18n.de.demoMD` und `i18n.en.demoMD`) auf den aktuellen Funktionsstand anpassen
   - Die Versionsnummer im Demo-Titel wird automatisch über `${APP_VERSION}` eingesetzt

5. **Lokal testen**
   - Datei in Chrome/Edge/Brave öffnen, alle Funktionen prüfen
   - In Firefox/Safari testen, Download-Fallback verifizieren
   - Sprachumschaltung, Theme-Wechsel, Drag & Drop, Scroll-Sync, Editor, Speichern, Export, Info-Button

6. **Commit-Nachricht**
   ```
   v26.X.Y: Kurze Beschreibung
   
   - Detaillierte Änderung 1
   - Detaillierte Änderung 2
   ```

7. **Push**
   ```bash
   git add -A
   git commit -m "v26.X.Y: ..."
   git push origin main
   ```

Der Workflow unter `.github/workflows/pages.yml` deployt anschließend automatisch auf GitHub Pages.

## Iteration zwischen Pushes

Kleinere Änderungen zwischen zwei Pushes erhöhen lediglich die Iterationszahl (`26.1.1 → 26.1.2`). Diese müssen nicht zwingend ins CHANGELOG aufgenommen werden, sollten aber in der `APP_VERSION` reflektiert sein, damit der aktuelle lokale Stand in der Fußzeile sichtbar bleibt.

## Code-Stil

- **Sprache der UI:** deutsch und englisch (vollständig über `i18n`-Mapping)
- **Sprache der Kommentare im Quelltext:** deutsch
- **Einrückung:** vier Leerzeichen
- **CSS-Custom-Properties** für sämtliche themenspezifischen Werte
- **Keine externen Build-Schritte** — der Viewer bleibt eine Single-File-Anwendung

## Sicherheit

- Eingehende Markdown-Inhalte werden konsequent durch `DOMPurify` sanitisiert
- Keine Cookies, kein `localStorage` mit Nutzerinhalten (nur UI-Präferenzen)
- Externe Skripte ausschließlich von `cdn.jsdelivr.net`
