# Mission Control Dashboard — Architektur

## Überblick
Ein komplettes "Mission Control" Dashboard für Leon & Bob — inspiriert vom OpenClaw Mission Control Konzept (roman.knox). Einzelne HTML/CSS/JS App mit Sidebar-Navigation und 6 Haupt-Screens.

## Screens (aus den Screenshots)

### 1. 📋 Tasks Board (Page 1/6)
- Kanban-Board: Backlog → In Progress → Review → Done
- Task-Karten mit: Titel, Assignee (Leon/Bob/Sub-Agent), Status, Priorität
- Stats oben: Total Tasks, In Progress, Done, Completion %
- Filter nach Assignee, Priorität, Projekt
- **Datenquelle:** `tasks.json` im workspace

### 2. 📝 Content Pipeline (Page 2/6)
- Pipeline-Stages: Ideas → Scripts → Thumbnails → Filming → Editing → Published
- Jeder Content-Eintrag: Titel, Stage, Beschreibung, Bilder
- Kann Skripte enthalten, editierbar
- **Datenquelle:** `content-pipeline.json`

### 3. 🧠 Memory (Page 3/6)
- Listet alle Memory-Dateien (MEMORY.md + memory/*.md)
- Schöne Document-Cards mit Preview
- Suchfunktion über alle Memories
- Journal-ähnliche Timeline-Ansicht
- **Datenquelle:** Liest tatsächliche Dateien aus workspace

### 4. 📅 Calendar (Page 4/6)
- Wochen/Monats-Ansicht
- Zeigt Cron Jobs, geplante Tasks, Deadlines
- Farbcodiert nach Typ (Routine, Deadline, Cron, Event)
- **Datenquelle:** `calendar.json` + Cron Jobs

### 5. 🏢 Office (Page 5/6)
- Digitales Büro — Pixel-Art oder isometrische Ansicht
- Jeder Agent hat einen Arbeitsplatz mit Avatar
- Status-Anzeige: Working / Idle / Offline
- Visuell sehen was gerade passiert
- **Datenquelle:** Agent-Status aus sessions

### 6. 👥 Team (Page 6/6)
- Meet the Team — Hierarchie-Ansicht
- Leon → Bob → Core Agents → Specialist Agents
- Rollen, Skills, Verantwortlichkeiten
- **Datenquelle:** `team.json` (basierend auf unserer bestehenden team-structure)

## Tech-Architektur

### Single-Page App (Vanilla)
- **Eine HTML-Datei** mit eingebettetem CSS + JS
- **Sidebar Navigation** links (wie im Screenshot)
- **Dark Theme** durchgehend
- **Kein Framework** — reines HTML/CSS/JS
- **LocalStorage** für Daten-Persistenz
- **JSON-Dateien** als Datenquelle (inline oder fetch)

### Layout
```
┌─────────┬──────────────────────────────┐
│         │  Header (Mission Control)     │
│ Sidebar │──────────────────────────────│
│         │                              │
│ Tasks   │  Main Content Area           │
│ Content │  (wechselt je nach Screen)   │
│ Memory  │                              │
│ Calendar│                              │
│ Office  │                              │
│ Team    │                              │
│         │                              │
│ Settings│                              │
└─────────┴──────────────────────────────┘
```

### Sidebar Items
- 🏠 Dashboard (Overview mit KPIs)
- 📋 Tasks
- 📝 Content Pipeline
- 🧠 Memory
- 📅 Calendar
- 🏢 Office
- 👥 Team
- ⚙️ Settings

### Design System
- **Farben:** Dark BG (#0a0a0f), Cards (#111827), Accent Cyan/Emerald
- **Font:** Inter oder System
- **Cards:** Glassmorphism, rounded, subtle border
- **Animations:** Smooth transitions, fade-in
- **Responsive:** Desktop-first, aber mobil nutzbar

### Initiale Daten (eingebettet)
Tasks, Calendar und Team-Daten werden als JSON im Script eingebettet, basierend auf Leons aktuellem Kontext:
- HostPro Dashboard MVP Tasks
- Kleinanzeigen-Automatisierung
- Gastgebertag Deadline (7. März)
- Team-Struktur wie bereits gebaut
- Morgenroutine, Training etc. im Calendar

## Dateien
```
mission-control/
├── index.html          # Komplette App
├── ARCHITECTURE.md     # Diese Datei
└── data/               # Optional: externe JSON-Dateien
    ├── tasks.json
    ├── content.json
    ├── calendar.json
    └── team.json
```
