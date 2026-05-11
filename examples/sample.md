# Beispieldokument

Dieses Dokument dient der Demonstration der Darstellungsmöglichkeiten des **MD-Viewers**. Es kann per Drag & Drop in das Anwendungsfenster gezogen werden.

## Strukturierte Inhalte

### Listen

Eine ungeordnete Aufzählung:

- Erster Punkt mit etwas mehr Text zur Demonstration der Zeilenumbrüche
- Zweiter Punkt
  - Unterpunkt mit Einrückung
  - Weiterer Unterpunkt
- Dritter Punkt

Eine geordnete Liste:

1. Vorbereitung der Daten
2. Durchführung der Analyse
3. Auswertung und Interpretation
4. Dokumentation der Ergebnisse

### Aufgabenliste

- [x] Versionierungsschema definiert
- [x] Fußzeile implementiert
- [x] Repository-Struktur erstellt
- [ ] Erster GitHub-Push
- [ ] Bekanntmachung der Anwendung

## Code-Beispiele

Inline-Code zur Hervorhebung: `const x = 42` oder `npm install`.

Block-Code mit Syntax-Highlighting:

```javascript
// Asynchrone Datei-Verarbeitung
async function processFile(file) {
    const text = await file.text();
    const parsed = marked.parse(text);
    const safe = DOMPurify.sanitize(parsed);
    return safe;
}
```

```python
def quicksort(arr):
    """Klassischer Quicksort-Algorithmus."""
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    return quicksort(left) + middle + quicksort(right)
```

## Mathematische Notation

Inline-Mathematik: Die Eulersche Identität $e^{i\pi} + 1 = 0$ verbindet fünf fundamentale Konstanten.

Block-Mathematik:

$$\int_{-\infty}^{\infty} e^{-x^2} \, dx = \sqrt{\pi}$$

$$\sum_{n=1}^{\infty} \frac{1}{n^2} = \frac{\pi^2}{6}$$

## Tabellen

| Algorithmus     | Beste Laufzeit  | Schlechteste    | Durchschnitt    |
|-----------------|-----------------|-----------------|-----------------|
| Bubble Sort     | $O(n)$          | $O(n^2)$        | $O(n^2)$        |
| Quicksort       | $O(n \log n)$   | $O(n^2)$        | $O(n \log n)$   |
| Merge Sort      | $O(n \log n)$   | $O(n \log n)$   | $O(n \log n)$   |
| Heap Sort       | $O(n \log n)$   | $O(n \log n)$   | $O(n \log n)$   |

## Zitate

> Die Wissenschaft ist der Aberglaube unserer Zeit.
>
> — *George Bernard Shaw*

## Hyperlinks

Weiterführende Hinweise finden sich in der [README](../README.md) sowie auf der [Webseite des Autors](https://www.michael-radeck.de).

---

*Eine bearbeitete Version dieser Datei kann über die Schaltfläche „Speichern" zurück in die Originaldatei geschrieben werden.*
