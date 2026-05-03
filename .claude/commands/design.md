# /design

Zeige Design-Entscheidungen und Spezifikationen aus DESIGN.md für einen Bereich.

## Verwendung
```
/design nav
/design dashboard
/design skills
/design recovery-sheet
/design profil
/design analyse
/design colors
/design typography
```

## Ablauf

### Schritt 1 – DESIGN.md lesen
Öffne DESIGN.md und finde den relevanten Abschnitt.

### Schritt 2 – Zusammenfassung ausgeben

```
🎨 Design-Spec: [Bereich]
━━━━━━━━━━━━━━━━━━━━━━━━

Layout:     [Beschreibung + ASCII-Skizze]
Farben:     [CSS Variablen]
Klassen:    .[klasse] – [Verwendung]
Animationen: [falls relevant]
```

### Schritt 3 – Wenn Bereich noch nicht in DESIGN.md
```
⚠️ Noch keine Design-Spec für [Bereich].
Soll ich eine vorschlagen?
```

## Design-System Kurzreferenz
```
Display:  Bebas Neue      → Titel, Hero-Zahlen
Data:     JetBrains Mono  → KPI-Werte, Labels, Tags
Body:     DM Sans         → Fließtext, Subtext

Farben: kraft #EF4444 · engine #22C55E · peak #F97316
        skills #A855F7 · struktur #3B82F6 · recovery #06B6D4

Readiness: Bereit #22C55E · Moderat #F97316 · Erholen #EF4444
```
