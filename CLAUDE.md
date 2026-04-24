# Project Doki Doki — A 100-Unit Project Management Learning Series

## Philosophy

The learner is never studying project management. They are following Ren, Saki, Tetsu, Director Kudo, and Hina through the chaos and triumphs of a high-stakes XR project — and absorbing PM frameworks, vocabulary, and judgment as they appear.

Every concept enters through a scene the learner cares about: a tense client meeting where Ren scrambles to define scope while Saki watches with barely concealed exasperation, a late-night war room where Tetsu is the only person who can fix the deployment, a retrospective where Hina's earnest notes accidentally surface the real problem. The PMBOK gives structure; The Phoenix Project gives urgency. The K-drama gives heart.

The series is designed for working or aspiring Project Managers who want to internalize both the formal discipline of PMBOK (process groups, knowledge areas, tools & techniques) and the pragmatic wisdom of The Phoenix Project (Theory of Constraints, The Three Ways, the Four Types of Work). By unit 100, the learner should be able to plan, execute, monitor, and close a real project — and know when to throw out the plan.

---

## Content Structure

### Two-Tier System

| Tier | File | Purpose |
|------|------|---------|
| **Meta Content** | `meta_content.csv` | 100-row spreadsheet defining every unit: pattern, scene, concepts, terms, review targets, subplot beats. This is the single source of truth. |
| **Unit Content** | `export/HTML/unit_XX.html` | Generated HTML files, one per unit. Each is a self-contained 2-page A5 printable document. |

### Cadence

| Phase | Units | Duration | Theme |
|-------|-------|----------|-------|
| Phase 1 — Foundations | 1–30 | ~10 weeks | Core PM concepts: lifecycle, stakeholders, charter, scope, schedule, cost, The Three Ways, WIP limits |
| Phase 2 — Application | 31–60 | ~10 weeks | Intermediate: Theory of Constraints, risk, quality, communications, change control, Kanban, agile, EVM |
| Phase 3 — Synthesis | 61–100 | ~14 weeks | Advanced: procurement, continuous improvement, DevOps, org change, benefits realization, portfolio alignment |

**Pace:** One unit every 2–3 days (~8.5 months total).

---

## Characters

### Ren (蓮) — The Proxy

- **Role:** Project Manager, Pulse Works (small XR studio, Company A)
- **Profile:** Early 30s. Resourceful, scrappy, learned PM by doing. Thinks frameworks are bureaucratic overhead — until they save him. Quick-witted, occasionally reckless. Hides stress behind humor.
- **Behavior style:** Informal, direct, action-first. Uses analogies and gut instinct. Skips documentation until it bites him. When stressed, makes unilateral decisions he later regrets.
- **Function:** The learner's stand-in. His mistakes are the learner's mistakes. His growth is the learner's growth. He starts as an intuitive but undisciplined PM and evolves into someone who wields frameworks with confidence.

### Saki (咲希) — The Challenger

- **Role:** Project Manager, Kurosawa Digital (large firm, Company B / the client)
- **Profile:** Late 20s. PMP-certified, sharp, process-driven. Sees Ren's chaos as unprofessional. Privately admires his creativity and ability to rally a team under pressure.
- **Behavior style:** Formal, precise, references PMBOK by name. Sends structured emails with numbered action items. Dislikes ambiguity. When frustrated, becomes icily polite. Her warmth leaks through in small moments — staying late to help, sending resources "for reference."
- **Function:** The force that introduces rigor. Her insistence on proper PM practice is how PMBOK concepts enter the narrative naturally. The tension between her structured approach and Ren's instincts creates productive conflict that teaches the learner both sides.

### Tetsu (哲) — The Bottleneck

- **Role:** Senior Developer / Tech Lead, Pulse Works
- **Profile:** Late 30s. Calm veteran engineer. The person everyone depends on — which is exactly the problem. Brilliant but overloaded. Doesn't complain; just works later.
- **Behavior style:** Quiet, precise, technical. Speaks in specifics, never generalities. Answers questions with questions. Protective of his team. Dry humor that surfaces only when he's comfortable.
- **Function:** Embodies the Theory of Constraints and The Phoenix Project's "Brent" archetype. His overload teaches WIP limits, resource planning, the danger of single points of failure, and the importance of knowledge transfer. His bottleneck status is the recurring systemic problem the characters must solve.

### Director Kudo (工藤部長) — The Stakeholder

- **Role:** VP of Digital Transformation, Kurosawa Digital
- **Profile:** 50s. Political, results-oriented. Doesn't care about process — only outcomes and optics. Changes scope on a whim to please the board. Charismatic in presentations, evasive in one-on-ones.
- **Behavior style:** Speaks in business outcomes and KPIs, never technical details. Uses phrases like "let's be strategic about this" and "I trust the team to figure it out" (meaning: do more with less). Praises publicly, pressures privately.
- **Function:** Teaches stakeholder management, communications management, change control, and managing up. Every interaction with Director Kudo is a lesson in navigating organizational politics. He is not a villain — he has real business pressures — but he makes the PM's job harder.

### Hina (陽菜) — The Mirror

- **Role:** Junior PM / Project Coordinator, Pulse Works
- **Profile:** Mid 20s. Eager, disorganized but lovable. Ren's mentee. Takes copious notes but can't always find them. Asks the "obvious" questions that turn out to be the right ones.
- **Behavior style:** Enthusiastic, slightly nervous, over-communicates. Uses too many exclamation points in chat messages. Volunteers for everything, struggles with prioritization. Grows visibly more competent across the series.
- **Function:** When Ren teaches Hina, the learner learns. Her mistakes are safe learning moments. Her growth mirrors the learner's journey. Her "naive" questions surface assumptions that experienced PMs overlook.

### Character Interaction Map

```
                    ┌─────────────┐
                    │ Director    │
                    │ Kudo        │
                    │ (Stakeholder)│
                    └──────┬──────┘
                           │ pressures / scope changes
                           ▼
    ┌──────────┐    ┌──────────┐
    │ Ren      │◄──►│ Saki     │
    │ (Proxy)  │    │(Challenger)│
    │ Pulse    │    │ Kurosawa  │
    │ Works    │    │ Digital   │
    └────┬─────┘    └──────────┘
         │ mentors        ▲
         ▼                │ reports to
    ┌──────────┐          │
    │ Hina     │    ┌─────┴────┐
    │ (Mirror) │    │          │
    │ Pulse    │    │          │
    │ Works    │    │          │
    └──────────┘    └──────────┘
         │
    ┌──────────┐
    │ Tetsu    │
    │(Bottleneck)│
    │ Pulse    │
    │ Works    │
    └──────────┘

  ◄──► = rivalry / romantic tension
  ──── = team / reporting relationship
```

---

## Unit Content Specification

### Section Types

#### Pattern A — Scenario + Concept Discovery Box

- **Scenario:** 8–12 lines of realistic PM dialogue/action. Settings include: client meetings, standups, planning sessions, war rooms, hallway conversations, Slack exchanges, retrospectives, vendor calls.
- **Concept Discovery Box:** 1–2 PM concepts that appeared in the scenario, explained with formal definitions, real-world context, and callouts to specific scenario lines. Blends PMBOK terminology with Phoenix Project wisdom where applicable.
- **Reading time:** ~4 minutes.

#### Pattern B — Reference Material + Key Concept Card

- **Reference Material:** A PM artifact (150–300 words) such as a project charter excerpt, status report, risk register entry, stakeholder email, Kanban board snapshot, change request form, vendor proposal, retrospective notes, scope document, or lessons learned log.
- **Key Concept Card:** 3–5 PM terms with: term name, formal definition, components/breakdown, 2–3 related terms, one example from the current or a prior scenario.
- **Reading time:** ~4 minutes.

#### Pattern C — Scenario + Key Concept Card + Review Corner

- **Scenario:** 8–10 lines (slightly shorter than Pattern A).
- **Key Concept Card:** 1–3 terms as in Pattern B.
- **Review Corner:** 2–3 mini-scenarios (2–3 lines each) that revisit concepts/terms from 4–8 units prior in new situations. Never repeats old scenes — always fresh context.
- **Reading time:** ~5 minutes.

### Rotation Pattern

| Pattern | Sections | Est. Reading |
|---------|----------|-------------|
| A | Scenario + Concept Discovery Box | ~4 min |
| B | Reference Material + Key Concept Card | ~4 min |
| C | Scenario + Key Concept Card + Review Corner | ~5 min |

Rotation: A → B → C → A → B → C → ...
Review every 3rd unit (Pattern C), reviewing material from 4–8 units prior.

---

## Progression Framework

### Phase 1 — Foundations (Units 1–30)

**Core Scenarios:**
- Ren's studio pitching for the Kurosawa Digital contract
- First client meetings with Saki (clash of styles)
- Setting up project governance and planning
- Early sprints and the first small wins
- First signs of Tetsu's overload

**Concepts Introduced:**
1. Project lifecycle & phases
2. Stakeholder identification & analysis
3. Project charter & business case
4. Scope definition & WBS
5. Requirements gathering
6. Schedule management & critical path
7. Resource planning & estimation
8. Cost management & budgeting
9. The Three Ways (flow, feedback, learning)
10. WIP limits

**Key Terms Target:** ~50 terms (5 per B/C unit)

**Reference Material Types:** `project_charter`, `stakeholder_email`, `scope_document`, `status_report`

**Character Focus:** Ren and Saki dominate. Hina appears in units 5+. Tetsu in units 8+. Director Kudo in units 12+.

**Subplot:** Ren and Saki's first meetings are combative. She corrects his documentation. He questions her rigidity. They argue about process vs. pragmatism. By unit 30, there's a moment of unexpected teamwork during a minor crisis — the first crack in the wall.

### Phase 2 — Application (Units 31–60)

**Core Scenarios:**
- Major scope change from Director Kudo
- Production incident / deployment failure
- Team burnout and resource conflicts
- Cross-team collaboration challenges
- Midpoint project health check

**Concepts Introduced:**
11. Theory of Constraints & bottleneck management
12. The Four Types of Work
13. Risk identification & response planning
14. Quality management
15. Communications management
16. Change control & integrated change management
17. Kanban & visual management
18. Agile & hybrid approaches
19. Earned value management (EVM)

**Key Terms Target:** ~50 terms

**Reference Material Types:** `risk_register`, `change_request_form`, `kanban_board`, `retrospective_notes`, `status_report`

**Character Focus:** Tetsu's bottleneck becomes critical. Director Kudo's scope changes create cascading problems. Saki and Ren are forced to collaborate closely.

**Subplot:** Working late nights together on the crisis. Ren sees Saki's vulnerability when Director Kudo publicly undermines her. Saki sees Ren's leadership when he protects his team. They start texting outside work hours — "just about the project." Neither admits what's happening. Hina notices everything.

### Phase 3 — Synthesis (Units 61–100)

**Core Scenarios:**
- Vendor failure and emergency procurement
- Organizational resistance to the XR platform
- DevOps transformation of the delivery pipeline
- Project near-cancellation and rescue
- Final delivery and retrospective

**Concepts Introduced:**
20. Procurement & vendor management
21. Continuous improvement & retrospectives
22. DevOps & deployment pipelines
23. Organizational change management
24. Benefits realization & project closure
25. Portfolio & program alignment

**Key Terms Target:** ~50 terms

**Reference Material Types:** `vendor_proposal`, `lessons_learned_log`, `change_request_form`, `status_report`, `retrospective_notes`, `kanban_board`

**Character Focus:** All five characters are fully active. Hina takes on real responsibility. Tetsu's bottleneck is finally resolved through systemic change, not heroics.

**Subplot:** The project faces cancellation. Ren and Saki must present a unified front to save it — which means trusting each other completely. A moment where Ren almost leaves the project, and Saki's reaction reveals her feelings. The confession happens during a quiet moment after a high-pressure steering committee. The project succeeds. The final unit is a retrospective — both for the project and the relationship.

---

## Formatting Specifications

- **Page size:** A5 portrait (148 × 210mm)
- **Margins:** 15mm all sides
- **Content width:** 118mm
- **Pages per unit:** 2 (strict maximum)
- **Body font:** Noto Sans, 9pt
- **Reference material font:** Noto Serif, 9pt
- **Heading font:** Noto Sans, bold
- **Output:** Self-contained HTML → browser Print → Save as PDF

---

## Meta Content CSV Schema

The `meta_content.csv` uses 18 columns:

```
index              — int, unit number (1–100)
phase              — int, 1/2/3
pattern            — str, "A"/"B"/"C"
scene_title        — str, short title for the unit's scenario/context
scene_title_sub    — str, subtitle or clarification
scene_desc         — str, 1-sentence scene description for the generator
characters         — str, comma-separated character names
concepts_new       — str, semicolon-separated new concepts introduced (Pattern A/C)
concept_prereqs    — str, comma-separated unit indices of prerequisite concepts
key_terms_new      — str, comma-separated key terms to introduce (Pattern B/C)
key_term_defs      — str, pipe-separated definitions matching key_terms_new order
reference_type     — str, type of reference material (Pattern B only)
reference_topic    — str, specific topic for reference material (Pattern B only)
review_concepts    — str, semicolon-separated concepts to review (Pattern C only)
review_terms       — str, comma-separated key terms to review (Pattern C only)
review_source      — str, comma-separated unit indices being reviewed (Pattern C only)
narrative_subplot  — str, subplot beat notes
notes              — str, special instructions for the generator
```

---

## Automation Architecture

### Prompt 1 — Meta Content Generator (One-Time)

**Purpose:** Generate the complete `meta_content.csv` with all 100 rows.

**Input:** This CLAUDE.md file.

**Output:** `meta_content.csv` following the schema above.

**Key constraints:**
- A→B→C rotation pattern, strictly maintained
- Concepts distributed across phases per the Progression Framework
- Prerequisites satisfied (no concept references concepts not yet introduced)
- Review callbacks in every Pattern C unit, targeting 4–8 units prior
- Narrative subplot beats woven per the phase descriptions
- Scene variety: no two consecutive units share the same setting

### Prompt 2 — Unit Content Generator (Per-Unit)

**Purpose:** Generate one HTML unit file per invocation.

**Input:** `meta_content.csv`, `GENERATE.md`, `STYLE_GUIDELINE.md`, `current_index.txt`

**Process:**
1. Read `current_index.txt` to determine which unit to generate
2. Parse the corresponding CSV row
3. Build cumulative concept and term sets from all prior rows
4. Generate content following `GENERATE.md` pattern rules
5. Assemble HTML following `STYLE_GUIDELINE.md` visual specifications
6. Write to `./export/HTML/unit_XX.html`
7. Increment `current_index.txt`

**Output:** `export/HTML/unit_XX.html` — a self-contained, printable A5 document.
