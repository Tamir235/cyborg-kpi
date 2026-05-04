# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

> Cyborg KPI – Hybrid Athlete Operating System
> Stand: Mai 2026 | Version: 3.0

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
- [ ] **P2-3: PR-Marker** – ▲ im Chart
- [ ] **P2-4: Touch-Targets** – min. 44×44pt
- [ ] **P2-5: Streak-Counter** – Dashboard

### 🟠 P3 – Navigation & UI Overhaul
- [ ] **NAV-1:** Nav Bar auf 4 Items umbauen
- [ ] **NAV-2:** Quick Log Sheet (6 Kacheln)
- [ ] **NAV-3:** Profil-Avatar oben rechts
- [ ] **NAV-4:** Recovery Sheet nach Training-Log
- [ ] **NAV-5:** Profil-Screen (Badges + PRs + Score-History)
- [ ] **NAV-6:** Analyse-Screen (Challenge + Radar + Streak)

### 🟠 P4 – Modul-Überarbeitung

#### Kraft ✅ Review
- [ ] K-1: Weighted Dips kg+Reps + Migration
- [ ] K-2: ATG Split kg+Reps
- [ ] K-3: Neue KPIs (Australian Rows, Archer, HBH, Nordic, One-Arm Hang)
- [ ] K-4: Progressive Unlock UI (B+E)
- [ ] K-5: Schmerz-Felder pro Übung
- [ ] K-6: Pistol → Skills migrieren

#### Struktur ✅ Review
- [ ] S-1: Dead Hang + Deep Squat + Mobility als separate KPIs
- [ ] S-2: Migration 5 bestehende Einträge

#### Skills ✅ Review
- [ ] SK-1: Focus Mode (C) + Skill Tree (A)
- [ ] SK-2: Alle 11 Gruppen
- [ ] SK-3: Cross-Unlocks (VSit→Manna, HBH→DF, HS→HSPU)
- [ ] SK-4: Milestone-Banner 80%

#### Engine ✅ Review
- [ ] E-1: Formular (Lauftyp, Distanz, Dauer, Pace auto, Kadenz, Temp)
- [ ] E-2: Neue KPIs
- [ ] E-3: Stats-Filter Lauftyp
- [ ] E-4: Migration (1 Eintrag → lauftyp:'zone2')

#### Peak ✅ Review
- [ ] PK-1: Formular (Protokoll Freitext, Dauer, Watt optional, RPE)

#### Recovery ✅ Review
- [ ] R-1: Stress + Muskelkater + Notizen (nur manuell)
- [ ] R-2 Phase 2: Health-API via Shortcuts/Export

### 🎮 P5 – Neue Features
- [ ] AD-1/2/3: Adaptive Empfehlung (regelbasiert via AIProvider)
- [ ] WC-1/2/3/4: Weekly Challenge (Impact-Berechnung, Badge)
- [ ] DNA-1/2: Skill DNA Blocker-Anzeige
- [ ] PRO-1/2: Badge-System + Profil-Screen
- [ ] AN-1/2/3/4: Analyse-Screen (Radar, Unlocks, Streak, Filter)

### 🟢 P6 – Polish & Design
- [ ] P6-1: Typografie (Bebas Neue + JetBrains Mono + DM Sans)
- [ ] P6-2: Y-Achse in Charts
- [ ] P6-3: Long-Press für Private Section
- [ ] P6-4: Haptic Feedback (PR + Unlock + Badge)
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
| Skills | ✅ | SK-1 bis SK-4 |
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
⚠️  HBH in Kraft UND Dragon Flag Basis
⚠️  Pistol: K-6 vor SK-2 implementieren
⚠️  Engine: Pace auto-berechnet (nie manuell eingeben)
⚠️  Badges: nie doppelt vergeben (ID-Check vor awardBadge)
⚠️  KI: immer AIProvider.getX() – nie direkter API-Call
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
