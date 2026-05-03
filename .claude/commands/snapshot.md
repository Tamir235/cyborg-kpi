# /snapshot

Erstelle einen Snapshot-Kommentar im Code der den aktuellen Stand dokumentiert.

## Ablauf

### Schritt 1 – Aktuellen Stand berechnen
- Cyborg-Score aus letztem Backup (falls vorhanden) oder aus Code
- Welche Module sind implementiert?
- Backlog-Fortschritt zählen

### Schritt 2 – Snapshot-Kommentar generieren

```javascript
// SNAPSHOT [Datum] · Score ~[X]% · Module: Kraft✅ Engine✅ Peak✅ Skills🔲 Struktur✅ Recovery✅
// Backlog: P1[0/3] P2[0/5] P3[0/6] · Nächster: [ID]
```

### Schritt 3 – Position fragen
```
Snapshot-Kommentar einfügen:
  a) Am Anfang des <script> Blocks
  b) Vor einer bestimmten Funktion
  c) Nur ausgeben (nicht einfügen)

Wo einfügen? (a/b/c)
```

### Schritt 4 – WARTEN auf Bestätigung, dann einfügen

## Verwendung
Nützlich um Meilensteine im Code zu markieren.
Besonders sinnvoll nach größeren Refactorings oder abgeschlossenen Phasen.

## Hinweis
Da index.html RTF-kodiert ist, muss der Kommentar entsprechend
escaped werden: `\/\/` statt `//` in bestimmten Kontexten nicht nötig –
normales `//` funktioniert im JS-Block.
