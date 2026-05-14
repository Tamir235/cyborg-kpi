# Cyborg KPI – Design Dokumentation
> Stand: Mai 2026 | Version: 2.1

---

## Design-Vision

**Cyborg Performance OS** – persönliches Kontrollzentrum, kein Standard-Fitness-UI.

**Adjektive:** präzise · dunkel · athletisch · systemisch · unvergesslich
**Nicht:** verspielt · generisch · überladen · Gaming-Trash

---

## Typografie

```
Display:  Bebas Neue      → Titel, Hero-Zahlen, Screen-Namen
Data:     JetBrains Mono  → KPI-Werte, Labels, System-Tags, Timestamps
Body:     DM Sans         → Fließtext, Beschreibungen, Subtext
```

**Regel:** Mono für alles was eine Zahl oder ein System-Label ist.

---

## Farbsystem

### System-Farben
```css
--kraft:    #EF4444
--engine:   #22C55E
--peak:     #F97316
--skills:   #A855F7
--struktur: #3B82F6
--recovery: #06B6D4
```

### Dark Mode
```css
--bg:    #111113
--bg2:   #161618
--card:  #1C1C1F
--card2: #232327
--card3: #2A2A2F
--rim:   rgba(255,255,255,.06)
--txt:   #F2F2F7
--txt2:  #98989F
--txt3:  #48484F
--blue:  #3B82F6
--blue2: #60A5FA
```

### Light Mode
```css
--bg:    #F2F2F7
--card:  #FFFFFF
--card2: #E5E5EA
--txt:   #000000
--sub:   #6C6C70
```

### Atmosphärische Details
- Grid-Texture Background (32px, 3% Opacity, nur Dark)
- Top-Line-Gradient auf Cards (Blue → transparent, 1px)
- Glow auf aktiven Elementen (box-shadow mit System-Farbe)
- Readiness-Dot: pulsierend (grün/orange/rot)

---

## Navigation – FINAL

### Nav Bar (4 Items)
```
⊞ HOME    + LOG    ✦ SKILLS    ◎ ANALYSE
```

**Log-Button:** Roter Akzent, mittig, größer als andere Items
**Aktiver Tab:** Blue Tint + Glow

### Quick Log Sheet
```
+ Button → Bottom Sheet
┌─────────────────────────────────────┐
│  ████████████████████  ← Handle    │
│                                     │
│  WAS TRAINIERST DU?                 │
│                                     │
│  ┌────────┐  ┌────────┐  ┌────────┐│
│  │  💪   │  │  🏃   │  │  ✦    ││
│  │ KRAFT │  │ENGINE │  │SKILLS ││
│  └────────┘  └────────┘  └────────┘│
│  ┌────────┐  ┌────────┐  ┌────────┐│
│  │  🏗   │  │  ⚡   │  │  ◎    ││
│  │STRUKT.│  │ PEAK  │  │RECOV. ││
│  └────────┘  └────────┘  └────────┘│
└─────────────────────────────────────┘
```

**Kachel-Design:**
- Hintergrund: System-Farbe mit 15% Opacity
- Border: System-Farbe mit 25% Opacity
- Icon: 24px zentriert
- Label: JetBrains Mono, 9px, ALL CAPS
- Tap: direkt Formular, kein Zwischen-Schritt
- Radius: 16px

### Recovery Sheet (kontextuell)
```
Erscheint 500ms nach Training-Log:

┌─────────────────────────────────────┐
│  ████████████  ← Handle            │
│                                     │
│  Training gespeichert 💪            │
│  Wie fühlst du dich?                │
│                                     │
│  Stress      [1]─────────────[10]  │
│  Muskelkater [1]─────────────[10]  │
│                                     │
│  [Notizen optional...]              │
│                                     │
│  [Speichern]    [Überspringen →]    │
│                                     │
│  auto-dismiss in 10s               │
└─────────────────────────────────────┘
```

**Design:**
- Background: `var(--recovery)` mit 8% Opacity als Akzent
- Border-Top: `var(--recovery)` mit 30% Opacity
- Sehr minimalistisch – nur 2 Slider + optional Text

### Profil-Zugang
```
Home Header rechts:
[Avatar-Icon 32px] → tippt → Profil-Screen

Avatar: Initialen des Users ODER Standard-Icon
        Kleiner Badge-Count wenn neue Badges
```

---

## Screen-Layouts

### Home (Dashboard)
```
Status Bar
┌─────────────────────────────────────┐
│ // SYSTEM_STATUS            [👤]    │ ← Profil-Zugang
│ Dashboard           (Bebas 32px)    │
│ Samstag, 2. Mai 2026                │
├─────────────────────────────────────┤
│ SCORE CARD                          │
│ [Ring 72px] | Cyborg Score          │
│              | Im Aufbau (18px 700) │
│              | // OUTRUN · OUTLIFT  │
│              | ▲ +3% Trend         │
│ [Mini Sparkline]                    │
├─────────────────────────────────────┤
│ WEEKLY CHALLENGE                    │
│ ⚡ Pull-ups auf 5 Reps              │
│ ████████░░  4/5  (80%)             │
│ Endet Sonntag                       │
├─────────────────────────────────────┤
│ HEUTE TRAINIEREN                    │
│ [●BEREIT] EMPFEHLUNG · KRAFT        │
│ Kraft-Training                      │
│ Pull-ups nah am PR · 7d Pause  [›] │
├─────────────────────────────────────┤
│ SYSTEME                             │
│ [2×3 Grid System-Cards]             │
└─────────────────────────────────────┘
Nav Bar: ⊞ + ✦ ◎
```

### Analyse
```
Status Bar
┌─────────────────────────────────────┐
│ // PERFORMANCE                      │
│ Analyse             (Bebas 32px)    │
├─────────────────────────────────────┤
│ [7 Tage] [4 Wochen] [12 Wochen]    │
├─────────────────────────────────────┤
│ WEEKLY CHALLENGE (erste Card)       │
│ ⚡ Pull-ups auf 5 Reps              │
│ ████████░░  4/5                    │
├─────────────────────────────────────┤
│ PERFORMANCE OVERVIEW                │
│ [Radar SVG – 6 Systeme]             │
├─────────────────────────────────────┤
│ SKILL UNLOCKS · NÄCHSTE STUFEN      │
│ ● Tuck Planche  ████░░  50%        │
│ ● One-Arm Hang  ████░░  50%        │
│ ● HSPU Wall     ░░░░░░  –          │
│ ● Archer Rows   ░░░░░░  –          │
├─────────────────────────────────────┤
│ KONSISTENZ · APRIL/MAI              │
│ [GitHub-Style 7×4 Grid]             │
│ [9 Sessions] [3 Streak] [32%]      │
└─────────────────────────────────────┘
Nav Bar: ⊞ + ✦ ◎(aktiv)
```

### Profil
```
Status Bar
┌─────────────────────────────────────┐
│ // ATHLETE                          │
│ Profil              (Bebas 32px)    │
├─────────────────────────────────────┤
│ SCORE HISTORY                       │
│ [Langzeit Chart alle Wochen]        │
│ 34% · Im Aufbau · Seit März 2026   │
├─────────────────────────────────────┤
│ BADGES                              │
│ [3-Spalten Grid]                    │
│ [🏆 gespeichert] [⭐ gesperrt]      │
├─────────────────────────────────────┤
│ PERSÖNLICHE REKORDE                 │
│ System  | KPI      | Wert | Datum  │
│ Kraft   | Pull-ups | 4    | 28.04  │
│ Skills  | Frog     | 40s  | 21.04  │
├─────────────────────────────────────┤
│ DATEN & EXPORT                      │
│ [JSON Export] [CSV Export]          │
│ [Backup] [Wiederherstellen]         │
└─────────────────────────────────────┘
Nav Bar: ⊞ + ✦ ◎
```

---

## Component Library

### Neu Navigation
```
.nav-bar              4-Item Bottom Bar
.nav-item             Einzelnes Item
.nav-item.active      Blue Tint + Glow
.nav-log-btn          Roter + Button (größer)
```

### Neu Sheets
```
.sheet-overlay        Blur Backdrop
.sheet                Bottom Sheet Container
.sheet-handle         Pill-Handle oben
.quick-log-grid       2×3 Kacheln
.quick-log-tile       Einzelne Kachel
.recovery-sheet       Recovery-spezifisches Sheet
.recovery-slider      Stress/Muskelkater Slider
```

### Neu Dashboard
```
.today-card           Adaptive Empfehlung
.readiness-dot        Pulsierender Indikator
.weekly-challenge     Challenge-Card
.challenge-bar        Fortschrittsbalken
.sys-grid             2×3 System-Kacheln
.sys-tile             Einzelne Kachel
```

### Neu Analyse
```
.radar-card           Radar-Chart Container
.streak-grid          GitHub-Style Grid
.streak-day           Einzelner Tag
.skill-prog-card      Unlock Progress
.sp-row               Einzelne Progress-Zeile
```

### Neu Profil
```
.badge-grid           3-Spalten Badge-Sammlung
.badge-item           Einzelner Badge
.badge-item.locked    Ausgegraut, gesperrt
.pr-table             PR-Übersicht
.score-history-card   Langzeit-Chart
```

### Neu Skills
```
.skill-focus-hero     Focus Hero Card (Auto-Fokus)
.skill-mini-grid      2×2 aktive Skills
.skill-tree-chain     Progressionskette
.skill-tree-node      Einzelner Node
.milestone-banner     80%-Unlock Hinweis
.dna-card             Skill DNA Blocker-Anzeige
.cross-unlock-toast   Cross-Unlock Toast
.tier-label           Tier 1 / Tier 2 Abschnittsheader
.foundation-chip      Referenz-Chip (crossRef zu anderen Systemen)
.chain-card           Collapsible Tier-2 Chain Card
.chain-header         Chain Name + Progress-Bar + Expand-Pfeil
.chain-nodes-flow     Horizontaler Node-Flow (nur expanded)
.cat-label            Kategorie-Label (PUSH / PULL / CORE / LEGS / BALANCE)
.fchain-step          Zwei-Schritt-Form: Step 1 (Kette wählen)
.fchain-skill-step    Zwei-Schritt-Form: Step 2 (Skill wählen)
```

---

## Readiness States

| State | Farbe | Dot | Empfehlung |
|---|---|---|---|
| Bereit | #22C55E | Pulsierend grün | Volles Training |
| Moderat | #F97316 | Pulsierend orange | Leichtes Training |
| Erholen | #EF4444 | Pulsierend rot | Active Recovery |

---

## Weekly Challenge Card

```css
/* Dashboard + Analyse (oben) */
background: rgba(59,130,246,.06);
border: 1px solid rgba(59,130,246,.2);
border-radius: 18px;

/* Bei Abschluss */
background: rgba(34,197,94,.08);
border-color: rgba(34,197,94,.25);
/* + Badge Flash Animation */
```

---

## Animationen

```css
@keyframes cardIn      { opacity + translateY 0.35s }
@keyframes fadeUp      { PR/Badge/Unlock Toast }
@keyframes unlockPop   { scale bounce – Skill Unlock }
@keyframes dotPulse    { Readiness-Dot: opacity + scale 2s infinite }
@keyframes badgeFlash  { Grüner Glow bei Challenge-Abschluss }
@keyframes sheetIn     { translateY(100%) → 0 – Bottom Sheet }
@keyframes sheetOut    { 0 → translateY(100%) }
```

---

## Haptic Feedback

```
haptic('light')   → 10ms           – Eintrag gespeichert
haptic('medium')  → 30ms           – Drag & Drop aktiviert
haptic('pr')      → 15 · 40 · 60ms – Neuer PR (doppelter Punch)
haptic('unlock')  → 20·30·20·30·80 – Skill Unlock (bereit für Badge-System)
haptic('badge')   → 30 · 20 · 70ms – Badge vergeben

Hinweis: Web Vibration API – funktioniert auf Android Chrome.
iOS Safari unterstützt die API nicht (kein Workaround ohne native App).
```

---

## Bekannte Design-Schulden

### 🔴 Accessibility
- Touch-Targets < 44pt (ibtn, db, mcl)
- Keine aria-labels
- --sub Kontrast ~3.5:1

### 🟡 UX
- Datum immer heute
- ~~Y-Achse in Charts fehlt~~ → ✅ implementiert (min/mid/max + Grid-Lines)
- PR-Marker im Chart fehlt
- Onboarding fehlt

---

## Versionshistorie

| Version | Datum | Änderung |
|---|---|---|
| 1.0–1.6 | Mai 2026 | Schrittweise Entwicklung |
| 2.0 | Mai 2026 | Premium-Redesign, neue Typo, alle Screens |
| 2.1 | Mai 2026 | Navigation final, Quick Log Sheet, Recovery Sheet, alle Component-Classes |
| 2.2 | Mai 2026 | Haptic Patterns dokumentiert, Y-Achse erledigt, dotPulse Animation |
| 2.3 | Mai 2026 | Skills Tier-Layout: Foundation-Chips, Tier-Labels, collapsible Chain-Cards, Kategorie-Labels, Zwei-Schritt-Form |
| 2.4 | Mai 2026 | Design Overhaul: Dark Palette (#111113 bg, #1C1C1F card), Grid-Texture BG (32px), Card Rim-Border + Blue Top-Gradient, Nav Active-Glow (blue), Log-Button Glow (red), System-Farben auf Spec (EF4444/22C55E/F97316/A855F7/3B82F6/06B6D4) |
