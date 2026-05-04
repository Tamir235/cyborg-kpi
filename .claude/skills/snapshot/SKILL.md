# /snapshot

Erstelle einen Snapshot-Kommentar im Code der den aktuellen Stand dokumentiert.

## Ablauf

### Schritt 1 – Stand berechnen
- Welche Module sind implementiert?
- Backlog-Fortschritt aus CLAUDE.md zählen

### Schritt 2 – Snapshot generieren

```javascript
// SNAPSHOT [Datum] · Module: Kraft✅ Engine✅ Peak✅ Skills🔲 Struktur✅ Recovery✅
// Backlog: P1[0/3] P2[0/5] P3[0/6] · Nächster: [ID]
```

### Schritt 3 – Position fragen
```
Snapshot einfügen:
  a) Am Anfang des <script> Blocks
  b) Nur ausgeben (nicht einfügen)
```

### Schritt 4 – WARTEN auf Bestätigung, dann einfügen
