# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

> Cyborg KPI – Hybrid Athlete Operating System
> Stand: Mai 2026 | Version: 4.0

---

## ✅ Skills-Migration abgeschlossen (04. Mai 2026)

Alle 20 Commands nach `.claude/skills/<name>/SKILL.md` migriert.
Originale in `.claude/commands/` bleiben als Backup erhalten.

---

## ⚡ Slash Commands → siehe SKILLS.md

---

## index.html – sauberes HTML (Stand: Mai 2026)

`index.html` ist **normales HTML** (648 Zeilen). Das RTF-Original liegt als Backup unter `backups/index-rtf-original.html`.

Entwicklung testen:
```
open index.html           # direkt im Browser öffnen (einfachste Methode)
python3 -m http.server 8000  # für PWA-Features (Service Worker etc.)
```

Es gibt keinen Build-Schritt, kein npm, keine Dependencies. Änderung speichern → Browser neuladen.

---

## Technische Architektur

### Einzel-Datei PWA

Alles in `index.html`: HTML, CSS und JS als IIFE. Kein externes Asset, kein Framework.

### State & Navigation

Navigation über einen **Stack**: `S.stack = [{type, sysId?, kpiK?}]`

```
Types: 'dash' | 'sys' | 'kpi' | 'stats' | 'daten' | 'private'
Push  → vorwärts navigieren
Pop   → S.stack.pop() → zurück
```

`render()` liest `S.stack[S.stack.length-1]` und baut `document.getElementById('app').innerHTML` vollständig neu auf.

Kein DOM-Patching. Jede Zustandsänderung → `lsSave(); render();`

### Zwei State-Objekte

```javascript
S   = { logs, targets, kpiOrder, stack, modal, period, ... }  // public
SEC = { unlocked, pwHash, logs, secModal, ... }                 // private (PE-Messungen)
```

### Zwei localStorage-Keys

```
'cyborg-v1'     → S (public)
'cyborg-sec-v1' → SEC (private, passwortgeschützt)
```

### Log-Eintrags-Strukturen

```javascript
// kraft
{ id, date, exercise: kpiK, value: number, technik: 1-5, pain: 0-10, notizen }

// engine
{ id, date, pace, hr, drift, rpe, nase: bool, notizen }

// peak
{ id, date, wattAvg, wattMax, rpe, notizen }

// skills
{ id, date, skill: kpiK, ist: number, qualitaet: 'ruhig'|'shaky', abbruch, notizen }

// struktur
{ id, date, hang, deepSquat, schulter, knie, ruecken, mobility: bool, notizen }

// recovery
{ id, date, hrv, notizen }

// SEC (private PE-Messungen)
{ id, date, bpsfl?, bpel?, nbel?, mseg?, beg?, notizen }
```

### KPI-Score-Berechnung

`sysSc(sysId, logs, targets)` → 0–1 (Durchschnitt aller KPI-Progressions)

`prog(val, kpi, targets, sysId)` → 0–1, wobei `hb:1` = higher-is-better

Cyborg-Score = Durchschnitt aller 6 Systeme × 100%

### Event-Handling

Einzelner click-Listener auf `#app` mit `data-a="action-name"` Delegation.
Alle Actions per `if(a==='...')` verarbeitet.

---

## Vision & Kernprinzip

**Cyborg KPI = Hybrid Athlete Operating System**

```
Nicht: "Was habe ich gemacht?"
Sondern: "Was soll ich heute tun und warum?"
```

**Leitprinzip:** OUTRUN THE LIFTERS · OUTLIFT THE RUNNERS

---

## Ehrliche Strategie (Stand Mai 2026)

**Kurzfristig/mittelfristig:** Persönliches Tool für einen User – mich.

Das bedeutet:
- Kein App Store, kein Support, kein Marketing
- Kein Android, kein Flutter, kein Swift (noch nicht)
- PWA ist die richtige Wahl – jetzt und für die nächsten Monate
- Komplexität darf hoch sein weil ich das System kenne

**Wenn sich das ändert:** Daten aus echter Nutzung entscheiden
ob und wie ein Produkt entsteht – nicht Spekulation.

---

## Fokussierte Roadmap

### Phase 1 – PWA fertigstellen (JETZT)
```
Single-File HTML · Claude Code schreibt alles
Regelbasierte KI · Kein Backend nötig
Alle Module implementieren · Design umsetzen
Ziel: Das beste persönliche Athleten-Tool
```

### Phase 2 – Backend + KI (in 6-12 Monaten)
```
Hetzner VPS · Node.js + Ollama (Mistral 7B)
Claude API für komplexe Analysen
HealthKit via Apple Shortcuts als Workaround
~€25/Monat · Narrative Empfehlungen
```

### Phase 3 – Entscheidung (wenn Phase 2 läuft)
```
Wenn persönliches Tool: native iOS App (Swift oder React Native)
Wenn Produkt: dann erst Flutter/Android Entscheidung treffen
Mit echten Nutzungsdaten – nicht mit Spekulation
```

---

## Technologie-Entscheidungen (für später dokumentiert)

### Wenn iOS only → React Native
- JavaScript (bereits bekannt)
- Claude Code kann es gut
- HealthKit, Watch, StoreKit verfügbar

### Wenn iOS + Android → Flutter
- Dart (einfach zu lernen)
- Eine Codebase für beide Plattformen
- Google ML Kit für Edge AI (TFLite)
- Bessere Performance als React Native

### Wenn Edge AI gewünscht
```
React Native: react-native-fast-inference → Core ML (iOS)
Flutter:      tflite_flutter → TFLite (iOS + Android)
              + Google ML Kit (direkt integriert)

Prinzip: AIProvider Interface bleibt gleich
Nur der Provider tauscht aus – Business-Code nie ändern
```

### Apple Intelligence (Phase 3+)
```
On-device · Kostenlos · <200ms · Datenschutz
iOS 18+ · Als Entwickler via Foundation Models API
Wird jährlich besser – 2027 Cloud-Qualität on-device
```

---

## KI-Architektur – AIProvider Interface

**Goldene Regel:** Nie direkter API-Call im Business-Code.
Immer über AIProvider – dann ist jeder Provider-Wechsel trivial.

```javascript
const AIProvider = {
  provider: 'mock', // Phase 1: 'mock' | Phase 2: 'claude'|'ollama'

  async getRecommendation(ctx) {
    if (this.provider === 'mock') return mockRecommendation(ctx);
    if (this.provider === 'claude') return claudeRecommendation(ctx);
    if (this.provider === 'ollama') return ollamaRecommendation(ctx);
  },

  async getPerformanceReport(data) { /* gleiche Struktur */ },
  async getDNAExplanation(skill, blockers) { /* gleiche Struktur */ }
}

// Phase 1 – Mock (regelbasiert, €0)
function mockRecommendation(ctx) {
  if (ctx.stress > 7 || ctx.muskelkater > 6)
    return { type:'recovery', text:'Active Recovery · Erhol dich heute' };
  if (ctx.daysSinceKraft > 5)
    return { type:'kraft', text:'Kraft-Training · ' + ctx.daysSinceKraft + 'd Pause' };
  if (ctx.unlockProgress > 0.8)
    return { type:'skills', text:'Skills · Unlock nah' };
  return { type:'kraft', text:'Kraft-Training' };
}
```

---

## App-Architektur

```
index.html  (RTF-Datei mit eingebettetem HTML)
└── <script> IIFE
    ├── Constants    COL, KPIS, SKILL_GROUPS, UNLOCK_RULES, SKILL_DNA
    │                LAUFTYPEN, BADGE_DEFS, AIProvider
    ├── State        S{} + SEC{}
    ├── Storage      lsLoad/lsSave/migrateAll()
    ├── AI           AIProvider (mock in Phase 1)
    ├── Calc         calcPace(), calcPaceHR(), calcImpact()
    │                getRecommendation(), generateChallenge()
    ├── Unlock       isUnlocked(), unlockProgress()
    ├── Badges       awardBadge(), checkMilestoneBadges()
    ├── DNA          getSkillBlockers()
    ├── Views        vDash, vSys, vKPI, vSkills, vSkillGroup
    │                vAnalyse, vProfil, vPE
    ├── Sheets       sheetQuickLog(), sheetRecovery()
    ├── Forms        fKraft, fEngine, fPeak, fSkills, fStruktur, fRecovery
    ├── Renderer     render() → innerHTML
    └── Events       click delegation
```

---

## Navigation – FINAL

```
Nav Bar: ⊞ HOME  + LOG  ✦ SKILLS  ◎ ANALYSE
Profil:  Avatar oben rechts im Home-Header
Recovery: Contextuelle Aktion nach Training-Log
Challenge: Dashboard (nach Empfehlung) + Analyse (erste Card)
Daten/Export: Untermenü im Profil-Screen
Quick Log: 6 Kacheln Bottom Sheet → direkt Formular
```

---

## Backlog – Implementierungs-Reihenfolge

### 🔴 P1 – JETZT STARTEN (Safety)
- [x] **P1-1: XSS-Escaping** – escHtml() + alle Freitext-Felder gesichert
- [x] **P1-2: Datum-Feld** – Date-Picker in allen 6 Forms
- [x] **P1-3: localStorage Quota** – Warning-Banner bei >80%

### 🟡 P2 – Core UX & Bugs
- [x] **P2-1: Bug Modal** – open-modal setzt fEx/fSkill aus KPI-Kontext
- [x] **P2-2: Input-Validierung** – Fehlermeldung bei 0-Werten
- [x] **P2-3: PR-Marker** – ▲ in Orange im Chart
- [x] **P2-4: Touch-Targets** – ibtn/mcl/db auf 44×44pt
- [x] **P2-5: Streak-Counter** – 🔥 Dashboard + Analyse
- [x] **P2-6: Eintrag-Schutz** – Grüner Undo-Toast 4s nach jedem Eintrag mit Rückgängig-Button
- [x] **P2-7: Weighted Dips Ansicht** – Reps als Hauptwert, kg als '@ Xkg' sekundär, Dual-Ziel (Reps + kg)

### 🟠 P3 – Navigation & UI Overhaul
- [x] **NAV-1:** Tabs → Home · Log · Profil · Analyse
- [x] **NAV-2:** Quick Log Sheet (S.sheet='quicklog', 6 Kacheln)
- [x] **NAV-3:** 👤 Avatar im Dashboard-Header
- [x] **NAV-4:** Recovery Sheet nach Training-Log (500ms, 10s auto-dismiss)
- [x] **NAV-5:** vProfil() – Score-History + PRs + Backup/Export
- [x] **NAV-6:** vAnalyse() – Radar-Chart + Streak-Grid + Skills-Progress

### 🟠 P4 – Modul-Überarbeitung

#### Kraft ✅ Review
- [x] K-1: Weighted Dips kg+Reps (wdReps in Meta)
- [x] K-2: ATG Split kg+Reps (atgReps in Meta)
- [x] K-3: Neue KPIs (Australian Rows, Archer, HBH, Nordic Curl, One-Arm Hang, Chest-to-Bar)
- [x] K-4: Progressive Unlock UI (KRAFT_UNLOCKS: archerRows/weightedDips/chestToBar/oneArmHang)
- [x] K-5: Schmerz-Labels pro Übung (PAIN_LABELS Map)
- [x] K-6: Pistol → Skills migriert (Migration + KPIS.skills)

#### Struktur ✅ Review
- [x] S-1: Mobility als separater KPI hinzugefügt
- [x] S-2: Migration boolean→numeric erledigt

#### Skills ✅ Review
- [x] SK-1: Focus Mode + Skill Tree (vSkillsHome, 6 Ketten, Fortschrittsbalken)
- [x] SK-2: 8 Ketten (Core Compression, Handstand, Planche, Pulling, Lever, Core Dynamic, Beine, Grip/Ring) + crossReqs + neue Skills chestToBar/falseGrip
- [x] SK-3: Cross-Unlock HBH→Dragon Flag (crossReq, crThreshold mit User-Ziel + minVal-Boden)
- [x] SK-4: Milestone-Banner 80% (inline in SK-1)
- [x] SK-5: Hybrid-Athlete Skill Tree Tier 1/2 Struktur (13 Chains: 3×Tier-1 + 10×Tier-2)
- [x] SK-6: 25 neue Skills-KPIs (37 gesamt, alle alten Keys erhalten, keine Migration nötig)
- [x] SK-7: Zwei-Schritt-Form (Kette → Skill), collapsible Tier-2 Chains, Foundation-Chips, Analyse-Filter

#### Engine ✅ Review
- [x] E-1: Formular (Lauftyp, Distanz, Dauer, Pace auto, Kadenz)
- [x] E-2: Distanz + Kadenz als neue Engine-KPIs
- [x] E-3: Lauftyp-Filter in Engine KPI-Ansicht
- [x] E-4: Migration lauftyp:'zone2' für alte Einträge

#### Peak ✅ Review
- [x] PK-1: Formular (Protokoll Freitext, Dauer, Watt optional, RPE required)

#### Recovery ✅ Review
- [x] R-1: Stress + Muskelkater als KPIs (Recovery Sheet speichert bereits)
- [ ] R-2 Phase 2: Health-API via Shortcuts/Export

### 🎮 P5 – Neue Features
- [x] AD-1/2/3: Adaptive Empfehlung (regelbasiert, 3 Zustände, pulsierender Dot, klickbar)
- [ ] AD-4: Empfehlung-Schwellenwerte prüfen nach echter Nutzung (Bereit: stress≤4/mkat≤4, Moderat: >4, Erholen: stress>7/mkat>6, Pause >3d)
- [x] WC-1/2/3/4: Weekly Challenge (schlechtestes System, 3 Sessions/Woche, Dashboard + Analyse)
- [x] DNA-1/2: Skill DNA Blocker-Anzeige (getSkillBlockers() + DNA-Sektion in vSkillsHome)
- [ ] PRO-1/2: Badge-System + Profil-Screen
- [ ] AN-1/2/3/4: Analyse-Screen (Radar, Unlocks, Streak, Filter)

### 🟢 P6 – Polish & Design
- [x] P6-1: Typografie (Bebas Neue Display, JetBrains Mono Data, DM Sans Body)
- [x] P6-2: Y-Achse in Charts (min/mid/max Labels + Grid-Lines, JetBrains Mono)
- [ ] P6-3: Long-Press für Private Section
- [x] P6-4: Haptic Feedback – haptic() helper + Save (light) + PR (double-buzz) + Drag (medium)
- [ ] P6-5: Empty-State / Onboarding

### ⚪ Phase 2 (Hetzner)
- Node.js, Ollama Mistral 7B, Claude Haiku API
- HealthKit Export-Workaround
- AIProvider.provider = 'ollama'

### ⚪ Phase 3 (entscheidung später)
- React Native (iOS only) oder Flutter (iOS+Android)
- HealthKit direkt, Watch, StoreKit
- Edge AI, Apple Intelligence

---

## Module-Review Status

| Modul | Status | Backlog |
|---|---|---|
| Kraft | ✅ | K-1 bis K-6 |
| Struktur | ✅ | S-1, S-2 |
| Skills | ✅ | SK-1 bis SK-7 |
| Engine | ✅ | E-1 bis E-4 |
| Peak | ✅ | PK-1 |
| Recovery | ✅ | R-1 |
| Navigation | ✅ | NAV-1 bis NAV-6 |
| KI-Architektur | ✅ | AIProvider dokumentiert |
| Business-Strategie | ✅ | Persönliches Tool, Phase 3 offen |

---

## Code-Standards

```javascript
// HTML-Injection – IMMER
function escHtml(s) {
  return String(s ?? '')
    .replace(/&/g,'&amp;').replace(/</g,'&lt;')
    .replace(/>/g,'&gt;').replace(/"/g,'&quot;');
}

// Neue Einträge – immer mit ID
{ id: uid(), date: todayISO(), ... }

// State + Save
S.x = y; lsSave(); render();

// KI – immer über AIProvider
const rec = await AIProvider.getRecommendation(ctx); // ✅
const res = await fetch('api.anthropic.com/...');     // ❌ nie direkt
```

---

## Häufige Fallstricke

```
⚠️  Quick Log Sheet ersetzt S.modal='pick'
⚠️  S.sheet = 'quicklog'|'recovery'|null (neues State-Feld)
⚠️  Recovery nicht in Nav – nur Sheet nach Training-Log
⚠️  Challenge: Dashboard + Analyse (beide!)
⚠️  Unlock-Status NIE in State cachen
⚠️  V-Sit = Cross-Unlock → Manna-Kette
⚠️  HBH = Hollow Body Hold (s) – in Kraft UND Dragon Flag Basis
⚠️  Pistol: K-6 vor SK-2 implementieren
⚠️  Engine: Pace auto-berechnet (nie manuell eingeben)
⚠️  Badges: nie doppelt vergeben (ID-Check vor awardBadge)
⚠️  KI: immer AIProvider.getX() – nie direkter API-Call
⚠️  SCROLL-BUG: render() setzt .content scrollTop auf 0!
    Bei Back-Nav IMMER vor render() speichern + danach restaurieren:
    var prevScroll=document.querySelector('.content')?.scrollTop||0;
    render();
    document.querySelector('.content').scrollTop=prevScroll;
```

---

## Testing-Checkliste

- [ ] Dark/Light Mode korrekt
- [ ] Quick Log Sheet alle 6 Systeme korrekt
- [ ] Recovery Sheet erscheint nach Training-Log
- [ ] Profil via Avatar erreichbar
- [ ] Challenge auf Dashboard + Analyse sichtbar
- [ ] Adaptive Empfehlung (3 Zustände: Bereit/Moderat/Erholen)
- [ ] Badge ohne Duplikate
- [ ] Radar-Chart korrekte Werte
- [ ] Migration ohne Datenverlust
- [ ] Export/Import JSON funktioniert

---

## Versionshistorie

| Version | Datum | Änderung |
|---|---|---|
| 1.0–1.6 | Mai 2026 | Module-Reviews |
| 2.0 | Mai 2026 | Vision, OS-Prinzip, Challenges, Badges |
| 2.1 | Mai 2026 | Navigation final, Quick Log Sheet |
| 2.2 | Mai 2026 | Phase 3, KI-Strategie, Free/Premium |
| 2.3 | Mai 2026 | Edge AI, AIProvider, HealthKit, Watch, StoreKit |
| 2.4 | Mai 2026 | React Native, Flutter, Vibe-Coding Pfad |
| 2.5 | Mai 2026 | Fokus: persönliches Tool · PWA first · Phase 3 offen |
| 2.6 | Mai 2026 | RTF-Kodierung dokumentiert, technische Architektur ergänzt |
| 2.7–2.8 | Mai 2026 | (intern, nicht dokumentiert) |
| 2.9 | Mai 2026 | Skills-Migration abgeschlossen (20/20), PreCompact auto-save Hook, RTF-Warnung bereinigt |
| 3.0 | Mai 2026 | P1 Safety komplett (XSS, Date-Picker, Quota), P2-1 Modal-Bug, P2-2 Input-Validierung |
| 3.1 | Mai 2026 | P2 komplett (PR-Marker, Touch-Targets, Streak), NAV komplett (NAV-1 bis NAV-6) |
| 3.2 | Mai 2026 | P4 Modul-Überarbeitung: K/S/E/PK/R alle Items außer K-4 + SK erledigt |
| 3.3 | Mai 2026 | P2-6 Undo-Toast, P2-7 WD Dual-Ansicht+Ziel, E-3 Lauftyp-Filter, HBH=Hollow Body Hold |
| 3.4 | Mai 2026 | SK-1 Focus Mode + Skill Tree, SK-3 Cross-Unlock HBH→Dragon Flag, SK-4 Milestone-Banner, /research Skill + calisthenics-wiki.md |
| 3.5 | Mai 2026 | SK-2 Skill Tree 8 Ketten + crossReqs, K-4 Progressive Unlock (KRAFT_UNLOCKS), chestToBar + False Grip KPIs, /research erweitert (Ernährung/Recovery/Kraft), wiki: Muscle-up + C2B + False Grip |
| 3.6 | Mai 2026 | AD-1/2/3 Adaptive Empfehlung (3 Zustände + pulsierender Dot), P6-1 Typografie (Bebas Neue + JetBrains Mono + DM Sans) |
| 3.7 | Mai 2026 | P6-2 Y-Achse in Charts (min/mid/max + Grid-Lines) |
| 3.8 | Mai 2026 | P6-4 Haptic Feedback (haptic() helper, Save/PR/Drag), WC-1/2/3/4 Weekly Challenge (Dashboard + Analyse) |
| 3.9 | Mai 2026 | DNA-1/2 Skill Blocker-Anzeige (getSkillBlockers()), fix: Scroll-Restaurierung bei Zurück-Nav, Recovery Sheet deaktiviert |
| 4.0 | Mai 2026 | SK-5/6/7 Hybrid-Athlete Skill Tree: Tier 1/2 Struktur, 37 KPIs (25 neu), 13 Chains, Zwei-Schritt-Form, Foundation-Chips, collapsible Tier-2, Analyse-Filter |
