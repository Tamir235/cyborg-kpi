# Cyborg KPI – Design Dokumentation
> Stand: Mai 2026 | Version: 4.3

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

### Dark Mode (v4.3 — Obsidian × Carbon Teal)
```css
--bg:    #090B0F   /* Deep blue-black — Carbon base */
--card:  #0E1118   /* Elevated surface */
--card2: #131820   /* Secondary surface */
--card3: #1A2030   /* Tertiary / borders */
--rim:   rgba(16,185,129,.07)
--txt:   #CBD5E1   /* Slate-200 */
--txt2:  #E2E8F0
--sub:   #4A5568   /* Slate-600 */
--sub2:  #3A4559
--brd:   #1A2030
--blue:  #10B981   /* Bio-Teal — primärer Akzent */
--blue2: #34D399   /* Teal-300 — sekundär */
--cyan:  #67E8F9   /* Cyan highlight (Ring-Tip) */
```

#### Textur
- Grid: `rgba(16,185,129,.025)` × 32px — Teal-getönt
- Carbon Weave: diagonale 45° Linien `rgba(255,255,255,.005)` × 10px
- Cards: `linear-gradient(to bottom, rgba(16,185,129,.06) 0px, rgba(16,185,129,0) 2px)` Top-Rim

#### Glow-System
```css
/* Primärer Teal-Glow */
box-shadow: 0 0 12px rgba(16,185,129,.5);

/* Score-Ring Glow */
filter: drop-shadow(0 0 6px rgba(16,185,129,.6));

/* System-Card Top-Line Glow */
box-shadow: 0 0 8px {systemColor}88;
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
- Grid-Texture Background (32px, teal-getönt) + Carbon-Weave (10px diagonal)
- Top-Rim auf Cards: Teal-Gradient, 2px
- System-Cards: Top-Line 1.5px mit System-Farbe + Glow
- Readiness-Dot: pulsierend (grün/orange/rot)
- Score-Ring: 100px SVG, Teal-Stroke, Bebas Neue Zahl innen
- Mantra-Bar: "Outlift the Runners · Outrun the Lifters" — JetBrains Mono, rgba(16,185,129,.4)

---

## Navigation – FINAL

### Nav Bar (4 Items)
```
⊞ HOME    + LOG    ✦ SKILLS    ◎ ANALYSE
```

**Log-Button:** Teal-Akzent (#10B981), quadratischer FAB (border-radius:4px), mittig, größer
**Aktiver Tab:** Teal Tint (#10B981) + Glow `box-shadow:0 0 12px rgba(16,185,129,.5)`
**Avatar-Button:** Runder Button, Teal-Border, Bebas Initiale

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

### Home (Dashboard) — v4.3
```
Status Bar
┌─────────────────────────────────────┐
│ 09:41                   ▮▮▮▮ 100% │
├─────────────────────────────────────┤
│ Dashboard           (Bebas 32px)  [T]│ ← Teal-Avatar
├─────────────────────────────────────┤
│ SCORE CARD                          │
│ ── Outlift the Runners · Outrun ──  │ ← Mantra-Bar, Mono, Teal-Lines
│ [Teal Ring 100px] | Cyborg Score   │
│  Bebas 40px Zahl  | Hybrid-Athlet  │
│  Score (Mono 9px) | 🔥 12  HRV 68  │
├─────────────────────────────────────┤
│ WEEKLY CHALLENGE (Teal Border)      │
│ ⚡ Engine — Zone 2 Focus            │
│ ████████░░  2/3                    │
├─────────────────────────────────────┤
│ EMPFEHLUNG (Border-Left Readiness)  │
│ [●] BEREIT · KRAFT                  │
│ Kraft-Training (Bebas 24px)        │
│ 3 Tage Pause (Mono 12px)           │
├─────────────────────────────────────┤
│ SYSTEME (3×2 Grid)                  │
│ ┌──────┐ ┌──────┐ ┌──────┐        │
│ │[Ring]│ │[Ring]│ │[Ring]│        │
│ │  78  │ │  65  │ │  52  │        │
│ │KRAFT │ │ENGIN │ │SKILL │        │
│ └──────┘ └──────┘ └──────┘        │
│ ┌──────┐ ┌──────┐ ┌──────┐        │
│ │  88  │ │  71  │ │  83  │        │
│ │STRUK │ │PEAK  │ │RECOV │        │
│ └──────┘ └──────┘ └──────┘        │
└─────────────────────────────────────┘
Nav Bar: ⊞ [+] ✦ ◎  (FAB: Teal square)
```

**System-Card Design:**
- 3-Spalten Grid
- Sharp border-radius: 14px
- Top-Line: 1.5px Systemfarbe + Glow
- Mini SVG-Ring (52px) mit Systemfarbe
- Bebas Neue Zahl (18px) in Ring-Center
- System-Name: JetBrains Mono 8px, uppercase, dimmed

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

## Animationen – Vollständige Referenz

### Implementierte Keyframes
```css
@keyframes cardIn   { from { opacity:0; transform:translateY(10px) scale(0.97) }
                      to   { opacity:1; transform:translateY(0) scale(1) } }
@keyframes fadeUp   { from { opacity:0; transform:translateX(-50%) translateY(8px) }
                      to   { opacity:1; transform:translateX(-50%) translateY(0) } }
@keyframes undoIn   { from { opacity:0; transform:translateX(-50%) translateY(6px) }
                      to   { opacity:1; transform:translateX(-50%) translateY(0) } }
@keyframes sheetIn  { from { transform:translateY(100%) } to { transform:translateY(0) } }
@keyframes slideDown{ from { transform:translateX(-50%) translateY(-100%) }
                      to   { transform:translateX(-50%) translateY(0) } }
@keyframes dotPulse { 0%,100% { opacity:1; transform:scale(1) }
                      50%     { opacity:.45; transform:scale(.75) } }
@keyframes ringFade { from { opacity:0 } to { opacity:1 } }
```

### Easing-Tokens (CSS Custom Properties)
```css
--ease-out:    cubic-bezier(0.23, 1, 0.32, 1)     /* Entering UI elements – stark, sofortiger Start */
--ease-drawer: cubic-bezier(0.32, 0.72, 0, 1)     /* iOS Bottom Sheet – authentischer Drawer-Curve */
```

**Warum diese Kurven?** Standard `ease` ist zu schwach und symmetrisch. `ease-out` startet sofort und bremst am Ende — der Nutzer sieht unmittelbare Reaktion. `ease-in` ist verboten: startet langsam → Interface fühlt sich träge an.

### Timing-Referenz

| Element | Dauer | Easing |
|---|---|---|
| Button Press | 120ms | `--ease-out` |
| Card Enter (`.anim`) | 300ms | `--ease-out` |
| Bottom Sheet | 280ms | `--ease-drawer` |
| Banner Slide-Down | 250ms | `--ease-out` |
| PR Toast | 280ms | `--ease-out` |
| Toggle | 150ms | `--ease-out` |
| Hover transitions | 100–150ms | `ease` |
| Readiness Dot Pulse | 2000ms | `ease-in-out` |

### Press Feedback – Pflicht auf jedem tappbaren Element
```css
.element { transition: transform 120ms var(--ease-out) }
.element:active { transform: scale(0.97) }  /* Buttons, Cards */
.nb:active { transform: scale(0.94) }        /* Nav-Buttons (kleiner) */
```

### Stagger-Delays (Card-Listen)
```css
.anim-d1 { animation-delay: .04s }  /* 40ms */
.anim-d2 { animation-delay: .08s }  /* 80ms */
.anim-d3 { animation-delay: .12s }  /* 120ms */
.anim-d4 { animation-delay: .16s }  /* 160ms — Maximum */
.anim-d5 { animation-delay: .16s }  /* gecapped */
.anim-d6 { animation-delay: .16s }  /* gecapped */
```

**Regel:** Maximum 160ms Stagger-Delay. Darüber fühlt sich der letzte Card zu spät an.

### Reduced Motion
```css
@media (prefers-reduced-motion: reduce) {
  .anim { animation: fadeIn .15s ease both }
  /* Nur Opacity, keine Transform-Motion */
}
```

---

## Animation Engineering – Prinzipien (Emil Kowalski)

> "All those unseen details combine to produce something that's just stunning, like a thousand barely audible voices all singing in tune." — Paul Graham

### Entscheidungsbaum: Soll etwas animiert werden?

| Häufigkeit | Entscheidung |
|---|---|
| 100+ mal/Tag (Keyboard Shortcuts, Command Palette) | **Keine Animation. Niemals.** |
| Dutzende mal/Tag (Hover, Listen-Navigation) | Entfernen oder stark reduzieren |
| Gelegentlich (Modals, Sheets, Toasts) | Standard-Animation |
| Selten / Erstkontakt (Onboarding, Celebrations) | Kann Delight hinzufügen |

### Goldene Regeln
- **Nur `transform` und `opacity` animieren** — GPU-beschleunigt, kein Layout-Thrashing
- **Niemals von `scale(0)` starten** — alles hat eine physische Form, auch wenn klein: `scale(0.95)` + `opacity:0`
- **Enter schnell, Exit noch schneller** — User wartet auf Enter, Exit soll sofort weg sein
- **Springs für Drag** — CSS-Transitions für Tap-Interaktionen (interruptible), Springs für Drag/Gesture
- **Hover nur auf Desktop** — immer mit `@media (hover:hover) and (pointer:fine)` wrappen

---

## CSS Standards

### Focus Rings (Accessibility — CRITICAL)
```css
.inp:focus  { border-color: rgba(59,130,246,.5) }
.sel:focus  { border-color: rgba(59,130,246,.5) }
.zinp:focus { border-color: rgba(59,130,246,.5) }
/* Alle Inputs: 1.5px solid transparent als Base, blauer Glow bei Focus */
```

### Schatten — Immer getönt, nie reines Schwarz
```css
/* ❌ Verboten */
box-shadow: 0 12px 40px rgba(0,0,0,.6);

/* ✅ Korrekt — getönt zum Hintergrund */
box-shadow: 0 12px 40px rgba(10,10,15,.75);

/* ✅ Farbiger Glow (System-Farbe) */
box-shadow: 0 0 12px rgba(59,130,246,.5);   /* blue active */
box-shadow: 0 4px 20px rgba(255,149,0,.4);  /* orange PR toast */
```

### Typografie-Qualität
```css
.pg-title { text-wrap: balance }        /* Keine Wörter allein auf letzter Zeile */
.f-mono, .pg-sub, .sec, .nl {
  font-variant-numeric: tabular-nums    /* Zahlen gleiche Breite → kein Layout-Shift */
}
```

### Hover — nur auf echten Zeigegeräten
```css
@media (hover:hover) and (pointer:fine) {
  .element:hover { /* hover styles */ }
}
/* Touch-Devices triggern hover auf Tap → false positives ohne diesen Guard */
```

---

## Design Audit Checkliste

Vor jedem Release oder Design-Review diese Punkte prüfen:

### 🔴 Kritisch (Accessibility)
- [ ] Kontrast ≥ 4.5:1 für normalen Text
- [ ] Focus-Ring sichtbar auf allen interaktiven Elementen
- [ ] Touch-Targets ≥ 44×44pt
- [ ] Kein `outline:none` ohne visuellen Ersatz
- [ ] `prefers-reduced-motion` Media Query vorhanden

### 🟡 Hoch (Interaktion)
- [ ] `:active` Scale-Feedback auf allen tappbaren Elementen
- [ ] Hover-States auf Desktop-Elementen (mit `(hover:hover)` Guard)
- [ ] Animationen nur mit `transform`/`opacity`
- [ ] Keine Duration über 300ms für UI-Animationen
- [ ] Keine `ease-in` Easing (fühlt sich träge an)

### 🟠 Mittel (Visuell)
- [ ] Schatten getönt (nicht `rgba(0,0,0,x)`)
- [ ] Stagger gecapped bei 160ms
- [ ] `tabular-nums` auf allen Zahlen-Displays
- [ ] `text-wrap: balance` auf Display-Headings
- [ ] `scroll-behavior: smooth` auf `html`

### 🟢 Niedrig (Polish)
- [ ] `min-height: 100dvh` (nicht `100vh` — iOS Safari Bug)
- [ ] Alle Inputs mit transparentem Border als Base (für Focus-Animation)
- [ ] Stagger-Delays korrekt gecapped

---

## Bekannte Design-Schulden

### 🔴 Accessibility
- ~~Touch-Targets < 44pt (ibtn, db, mcl)~~ → `.ibtn` font 9px → 11px ✅, `.mcl` 44×44 ✅
- Keine `aria-label` auf Icon-Buttons
- `--sub` Kontrast ~3.5:1 (unter WCAG AA)

### 🟡 UX
- Datum-Feld: immer heute vorausgefüllt, keine manuelle Anpassung ohne DatePicker
- PR-Marker im Chart fehlt (P2-3 markiert als erledigt, aber visuell prüfen)
- Onboarding / Empty States fehlen (P6-5)

### ✅ Behoben diese Session
- Y-Achse in Charts → ✅
- `outline:none` auf Inputs → ✅ Focus Rings hinzugefügt
- Press Feedback auf Buttons → ✅ `:active` scale
- Sheet Entry Animation → ✅ iOS Drawer Curve
- Drag Ghost Shadow → ✅ getönt
- Hover auf Desktop-Elementen → ✅ mit Guard
- `tabular-nums` → ✅
- `scroll-behavior:smooth` → ✅

---

## Haptic Feedback

```
haptic('light')   → 10ms            – Eintrag gespeichert
haptic('medium')  → 30ms            – Drag & Drop aktiviert
haptic('pr')      → 15 · 40 · 60ms  – Neuer PR (doppelter Punch)
haptic('unlock')  → 20·30·20·30·80  – Skill Unlock
haptic('badge')   → 30 · 20 · 70ms  – Badge vergeben

Platform: Web Vibration API — Android Chrome ✅, iOS Safari ❌ (kein Workaround ohne native App)
```

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
| 3.0 | Mai 2026 | Blueprint-Erweiterung: vollständige Animation-Referenz, Easing-Tokens, Emil-Prinzipien, CSS Standards (Focus, Shadows, tabular-nums), Design Audit Checkliste, Schulden-Update |
