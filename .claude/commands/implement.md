# /implement

Implementiere einen Backlog-Item sicher und strukturiert.

## Verwendung
```
/implement P1-1
/implement NAV-2
/implement K-1
```

## Ablauf

### Schritt 1 – Item verstehen
- Lies den Backlog-Item aus CLAUDE.md
- Erkläre in 2-3 Sätzen was geändert wird und warum
- Prüfe ob Abhängigkeiten existieren (z.B. K-6 vor SK-2)

### Schritt 2 – Code-Stelle finden
- Öffne index.html
- Finde die relevanten Stellen
- Zeige den aktuellen Code

### Schritt 3 – Diff anzeigen
Zeige exakt was geändert wird:

```
VORHER:
[alter Code]

NACHHER:
[neuer Code]
```

### Schritt 4 – WARTEN
Schreibe NICHT bevor der User bestätigt hat.
Akzeptierte Bestätigungen: "ja", "ok", "mach es", "go", "✓"

### Schritt 5 – Implementieren
- Schreibe die Änderung in index.html
- Erkläre kurz was geändert wurde

### Schritt 6 – Testing-Hinweis
Gib konkrete Test-Schritte aus:
```
Teste jetzt:
□ [Spezifischer Test 1]
□ [Spezifischer Test 2]
□ Dark Mode korrekt
□ Reload lädt Daten korrekt
```

## Wichtige Regeln
- NIEMALS direkt schreiben ohne Bestätigung
- Bei Datenstruktur-Änderungen: Migration prüfen
- Bei neuen State-Feldern: lsSave() nicht vergessen
- Escape User-Inputs immer mit escHtml()
- Unlock-Status NIE in State cachen
