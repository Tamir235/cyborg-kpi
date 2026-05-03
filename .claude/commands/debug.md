# /debug

Systematische Fehlersuche für ein gemeldetes Problem.

## Verwendung
```
/debug "Modal zeigt falsche Übung"
/debug "Score wird nicht korrekt berechnet"
/debug "Eintrag wird nicht gespeichert"
```

## Ablauf

### Schritt 1 – Problem verstehen
- Beschreibe genau was passiert
- Beschreibe was stattdessen passieren soll
- In welchem Screen / bei welcher Aktion tritt es auf?

### Schritt 2 – Code analysieren
- Finde den relevanten Event-Handler in index.html
- Trace den Datenfluss: User-Aktion → State → render()
- Suche nach dem Punkt wo es abweicht

### Schritt 3 – Hypothese
```
Vermutliche Ursache: [Erklärung]
Betroffene Zeilen: [ca. Zeilennummern]
```

### Schritt 4 – Fix vorschlagen
Zeige Diff (VORHER/NACHHER) und warte auf Bestätigung.

## Häufige Bug-Quellen
```
Modal falsche Übung:  S.fEx nicht aus KPI-Kontext gesetzt
Eintrag verschwindet: lsSave() fehlt nach State-Mutation
Score falsch:         sysSc() berechnet aus falschen Logs
Unlock falsch:        isUnlocked() cached State (nie cachen!)
Chart leer:           getEnts() gibt falsches Format zurück
PR nicht erkannt:     hb-Flag falsch gesetzt
Migration failed:     _migrated Flag nicht gesetzt
```

## DevTools Hinweise
```javascript
// In Browser-DevTools prüfen:
JSON.parse(localStorage.getItem('cyborg-v1'))
// → Zeigt alle gespeicherten Daten

// State live checken:
// In index.html am Ende der IIFE hinzufügen:
window.S = S; // dann in Konsole: S.logs
```
