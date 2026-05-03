# /refactor

Schlage Refactoring für eine Funktion vor ohne ihr Verhalten zu ändern.

## Verwendung
```
/refactor vDash
/refactor renderModal
/refactor getEnts
/refactor addEntry
```

## Ablauf

### Schritt 1 – Funktion analysieren
- Lies die Funktion in index.html
- Messe: Wie viele Zeilen? Wie viele Verantwortlichkeiten?

### Schritt 2 – Probleme identifizieren
```
📊 Analyse: [Funktionsname]
━━━━━━━━━━━━━━━━━━━━━━━━
Zeilen:          [N]
Verantwortl.:    [N] (Faustregel: max. 1-2)
Verschachtelung: [Tief / Mittel / Flach]

Probleme:
  → [Problem 1]
  → [Problem 2]
```

### Schritt 3 – Vorschlag machen
- Wie könnte man aufteilen?
- Welche Hilfsfunktionen würden entstehen?
- Zeige das Refactoring als Diff

### Schritt 4 – WARTEN auf Bestätigung

### Schritt 5 – Implementieren

## Regeln
- Kein Verhalten ändern – nur Struktur
- Keine neuen Features einbauen
- Tests (manuell) müssen identisches Ergebnis zeigen
- Bevorzuge: Extraktion von reinen Hilfsfunktionen
- Vermeide: Abstraktion für hypothetische Zukunft

## Wann refactorn?
- Funktion > 50 Zeilen → Kandidat
- Funktion > 100 Zeilen → refactorn
- Gleicher Code-Block 3× wiederholt → Extraktion
