# /design

Zeige Design-Entscheidungen und Spezifikationen aus DESIGN.md für einen Bereich.

## Verwendung
```
/design unlock
/design nav
/design dashboard
/design skills
/design recovery-sheet
/design profil
/design analyse
/design typography
/design colors
```

## Ablauf

### Schritt 1 – DESIGN.md lesen
Öffne DESIGN.md und finde den relevanten Abschnitt.

### Schritt 2 – Zusammenfassung ausgeben

```
🎨 Design-Spec: [Bereich]
━━━━━━━━━━━━━━━━━━━━━━━━

Layout:
  [Beschreibung + ASCII-Skizze falls vorhanden]

Farben:
  Hintergrund: [CSS Variable]
  Akzent:      [CSS Variable oder System-Farbe]
  Text:        [CSS Variable]

CSS-Klassen:
  .[klasse]   – [Verwendung]

Animationen:
  [falls relevant]

Bekannte Design-Schulden:
  [falls vorhanden]
```

### Schritt 3 – Wenn Bereich noch nicht in DESIGN.md
```
⚠️ Noch keine Design-Spec für [Bereich].
Soll ich eine vorschlagen basierend auf dem bestehenden Design-System?
```

## Design-System Kurzreferenz
```
Display:  Bebas Neue      → Titel, Hero-Zahlen
Data:     JetBrains Mono  → KPI-Werte, Labels, Tags
Body:     DM Sans         → Fließtext, Subtext

System-Farben: kraft #EF4444 · engine #22C55E · peak #F97316
               skills #A855F7 · struktur #3B82F6 · recovery #06B6D4

Readiness: Bereit #22C55E · Moderat #F97316 · Erholen #EF4444
```
