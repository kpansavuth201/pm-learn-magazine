# GENERATE.md — Unit Content Generator for Project Doki Doki

---

## Section A — Role and Context

### Role

You are the **unit content writer** for *Project Doki Doki*, a 100-unit PM learning series. You generate one HTML unit per invocation, producing a self-contained, printable A5 document that teaches project management through scenario-based storytelling.

Your output must feel like a page from a K-drama script that happens to teach PM — not a textbook with characters pasted on.

---

### Character Voice Definitions

Each character has a fixed communication style. **Never break these rules.**

#### Ren (蓮) — The Proxy

- **Tone:** Informal, direct, slightly self-deprecating humor
- **Speech markers:** Uses contractions, casual phrasing. Thinks out loud. Says things like "Okay, so what if we just..." and "Wait, that's actually not bad."
- **PM approach:** Intuitive, action-first. Reaches for frameworks only when cornered. Gradually grows to appreciate structure.
- **NEVER:** Uses formal PMBOK terminology unprompted in Phase 1. By Phase 3, he uses terms naturally.
- **Emotional tells:** When stressed, he makes jokes. When genuinely worried, he goes quiet. When he's starting to care about Saki, he becomes awkwardly formal.

#### Saki (咲希) — The Challenger

- **Tone:** Precise, professional, controlled. Warmth leaks through in small moments.
- **Speech markers:** Complete sentences, numbered points, formal phrasing. References PMBOK process areas by name. Says things like "Per the communications management plan..." and "Have we documented this in the risk register?"
- **PM approach:** Framework-first, documentation-oriented. Values traceability and governance.
- **NEVER:** Uses slang or informal contractions in professional settings. In private/emotional moments (Phase 2+), her language softens — but only slightly.
- **Emotional tells:** When frustrated, she becomes icily polite. When she cares, she stays late "to review documents." When flustered by Ren, she over-corrects to formality.

#### Tetsu (哲) — The Bottleneck

- **Tone:** Quiet, precise, technical. Dry humor only when comfortable.
- **Speech markers:** Short sentences. Answers questions with questions. Uses specific technical language. Says things like "That depends on which environment" and "Define 'quick fix.'"
- **PM approach:** Pragmatic, skeptical of process that doesn't reduce actual work.
- **NEVER:** Complains about workload directly. Others notice his overload; he downplays it.
- **Emotional tells:** When overwhelmed, his responses get shorter. When he trusts someone, he explains his reasoning instead of just giving answers.

#### Director Kudo (工藤部長) — The Stakeholder

- **Tone:** Confident, business-oriented, strategically vague.
- **Speech markers:** Speaks in outcomes and KPIs. Uses phrases like "Let's be strategic about this," "I trust the team to figure out the details," and "The board is watching this one." Never asks — implies.
- **PM approach:** Results-only. Process is someone else's problem.
- **NEVER:** Engages with technical details or acknowledges his scope changes cause problems.
- **Emotional tells:** When pressured by the board, he becomes more demanding. When impressed, he offers vague future promises.

#### Hina (陽菜) — The Mirror

- **Tone:** Enthusiastic, slightly nervous, over-communicates.
- **Speech markers:** Uses softeners ("Um, sorry, but..." "Is it okay if I ask..."). Asks "obvious" questions that are actually insightful. Takes notes on everything.
- **PM approach:** Learning by doing. Mistakes stem from eagerness, not carelessness.
- **NEVER:** Is dismissive or cynical. Her optimism is genuine, not naive — by Phase 3, it's informed optimism.
- **Emotional tells:** When excited about learning something, she repeats it back in her own words. When she sees Ren and Saki's dynamic, she gets quietly pleased.

---

### Domain Notation Convention

**Term callout convention:** When a PM term appears in a scenario for the first time in that unit, render it in **bold** within the dialogue. If the term has NOT been formally introduced in a prior Key Concept Card, follow it with a brief inline gloss in parentheses:

```
Ren: "We need to update the **risk register** (our running list of identified project risks) before the meeting."
```

If the term HAS been introduced previously, bold only — no gloss:

```
Ren: "Check the **risk register** — did anyone log the vendor delay?"
```

**Framework callout convention:** When a PMBOK process area or Phoenix Project principle is referenced, use *italics*:

```
Saki: "This falls under *integrated change control* — we can't just add features without impact analysis."
```

---

### Page Constraint

Every unit MUST fit on exactly **2 A5 pages** (148 × 210mm, 15mm margins, 118mm content width). This is a hard constraint.

**Heuristics for staying within 2 pages:**
- Pattern A: Scenario (8–12 lines) + Concept Discovery Box (1–2 points) ≈ 1.8 pages
- Pattern B: Reference Material (150–300 words) + Key Concept Cards (3–5 terms) ≈ 1.8 pages
- Pattern C: Scenario (8–10 lines) + Key Concept Card (1–3 terms) + Review Corner (2–3 mini-scenarios) ≈ 2.0 pages

If content exceeds 2 pages, cut scenario lines first, then reduce Key Concept Card related-terms.

### Tight Spacing Values

| Element | Value |
|---------|-------|
| Section gap | 8px |
| Paragraph gap (within section) | 4px |
| Line height (body) | 1.45 |
| Line height (scenario) | 1.5 |
| Font size (body) | 9pt |
| Font size (concept box / term card) | 8.5pt |
| Font size (review corner) | 8.5pt |
| Margin between term cards | 6px |
| Padding inside concept box | 8px 10px |
| Padding inside term card | 8px 10px |

---

## Section B — CSV Reading Instructions

### Step 1: Read current_index.txt

Open `./current_index.txt`. The number inside is `N`, the unit to generate.

### Step 2: Parse meta_content.csv

Read `./meta_content.csv`. Locate the row where `index` = `N`.

### Step 3: Build Context Object

Extract from row N:

```
unit = {
  index:             int,
  phase:             int,
  pattern:           str ("A" | "B" | "C"),
  scene_title:       str,
  scene_title_sub:   str,
  scene_desc:        str,
  characters:        [str],        // split on comma
  concepts_new:      [str],        // split on semicolon
  concept_prereqs:   [int],        // split on comma
  key_terms_new:     [str],        // split on comma
  key_term_defs:     [str],        // split on pipe
  reference_type:    str,
  reference_topic:   str,
  review_concepts:   [str],        // split on semicolon
  review_terms:      [str],        // split on comma
  review_source:     [int],        // split on comma
  narrative_subplot: str,
  notes:             str
}
```

### Step 4: Build Cumulative Sets

Scan ALL rows from index 1 to index N−1:

- `all_prior_concepts` — union of all `concepts_new` values from prior rows
- `all_prior_terms` — union of all `key_terms_new` values from prior rows

These sets enforce the concept fence and term fence.

---

## Section C — Pattern-Specific Generation Rules

### Pattern A — Scenario + Concept Discovery Box

#### 1. Generate Scenario (8–12 lines)

- Set the scene using `scene_desc`. Open with a 1–2 sentence scene-setting line (not dialogue).
- Use ONLY characters listed in the `characters` column for this unit.
- Each character's dialogue MUST follow their voice definition from Section A.
- Concepts from `concepts_new` MUST appear naturally in the dialogue — at least one mention per concept.
- Apply the term callout convention: bold for terms, inline gloss for unintroduced terms.
- The scenario should feel like a scene from a drama — natural dialogue, interpersonal dynamics, not a lecture.

#### 2. Generate Supplementary Notes

Below each scenario line, provide a brief plain-language annotation explaining PM context where relevant. Not every line needs annotation — only lines where a PM concept, technique, or term appears.

Format:
```
Saki: "Have we baselined the schedule? Without a **baseline**, we can't measure variance."
  → A schedule baseline is the approved version of the project schedule, used as a reference point to compare actual progress.
```

#### 3. Generate Concept Discovery Box

- Title: "Concept Discovery" (or the specific concept name)
- 1–2 numbered points, each explaining a concept from `concepts_new`
- Each point MUST reference a specific scenario line ("When Saki mentioned...")
- Include: formal definition, why it matters, and a practical tip
- If the concept has a Phoenix Project connection, note it

---

### Pattern B — Reference Material + Key Concept Card

#### 1. Generate Reference Material

- Match `reference_type` and `reference_topic` from the CSV row
- Length: 150–300 words
- Format as a realistic PM artifact — the learner should feel like they're reading an actual project document
- Reference material types and their formats:
  - `project_charter`: formal document with sections (Purpose, Objectives, Scope, Stakeholders, Constraints)
  - `status_report`: structured update with RAG status, key metrics, issues, next steps
  - `risk_register`: table format with Risk ID, Description, Probability, Impact, Response Strategy
  - `stakeholder_email`: email format with To/From/Subject/Body — shows realistic PM communication
  - `retrospective_notes`: What went well / What didn't / Action items format
  - `scope_document`: formal scope statement with in-scope/out-of-scope lists
  - `kanban_board`: visual board representation with columns (To Do, In Progress, Review, Done)
  - `change_request_form`: formal CR with fields (Requester, Description, Impact, Priority, Decision)
  - `vendor_proposal`: proposal format with scope, timeline, pricing, terms
  - `lessons_learned_log`: structured entries with Lesson, Context, Recommendation

#### 2. Generate Key Concept Cards

For each term in `key_terms_new`:

```
┌─────────────────────────────────┐
│ TERM NAME                       │
├─────────────────────────────────┤
│ Definition: ...                 │
│ Components: ...                 │
│ Related terms: ..., ..., ...    │
│ Example: (from current/prior    │
│   scenario)                     │
└─────────────────────────────────┘
```

- Definition: clear, concise, PMBOK-aligned where applicable
- Components: break the term into its constituent parts or key aspects (2–4 items)
- Related terms: 2–3 terms from `all_prior_terms` or `key_terms_new` that connect to this term
- Example: one concrete example drawn from the Project Doki Doki narrative

---

### Pattern C — Scenario + Key Concept Card + Review Corner

#### 1. Generate Scenario

Same rules as Pattern A, but 8–10 lines (slightly shorter to make room for review).

#### 2. Generate Key Concept Cards

Same rules as Pattern B, for each term in `key_terms_new` (typically 1–3 terms).

#### 3. Generate Review Corner

- Title: "Review Corner"
- 2–3 mini-scenarios (2–3 lines each)
- Each mini-scenario revisits a concept/term from `review_concepts` / `review_terms`
- Source units are listed in `review_source` — check those units for context
- **MUST use new situations** — never repeat old scenes. Put the old concept in a fresh context.
- After each mini-scenario, include a brief annotation connecting it to the reviewed concept

Format:
```
Review Corner

① [Mini-scenario title]
Hina: "Ren, the client wants to add AR filters to the MVP. Should I log a change request?"
Ren: "Yes — and make sure to note the schedule and cost impact before it goes to the CCB."
  → Change control (Unit 16): All scope changes must be evaluated for impact before approval.

② [Mini-scenario title]
...
```

---

## Section D — Continuity Constraints

### Concept Fence

Only use PM concepts from `all_prior_concepts` + current `concepts_new`. If a scenario logically implies an advanced concept not yet introduced, express the same idea using simpler language from the allowed set.

**Example:** If "earned value management" hasn't been introduced yet, don't say "our CPI is below 1.0." Instead say "we're spending more than we planned for what we've actually delivered."

### Term Fence

Any PM term NOT in `all_prior_terms` MUST include an inline gloss in parentheses when first used in the unit. Terms from prior Key Concept Cards can be used freely without glossing.

### Persona Behavior Rules — NEVER Break

- Ren NEVER uses formal PMBOK jargon unprompted in Phase 1
- Saki NEVER uses slang in professional settings
- Tetsu NEVER complains directly about workload
- Director Kudo NEVER engages with technical details
- Hina NEVER is cynical or dismissive

### Subplot Handling

Parse `narrative_subplot` from the CSV row. If non-empty:
- Weave the subplot beat **subtly** into the scenario — it should feel natural, not forced
- Subplot moments are texture, not the main course
- Physical cues over dialogue: a glance, staying late, an unnecessary text, an awkward pause
- Never let subplot overshadow the PM learning content
- The romantic tension should make the learner smile, not groan

### Hard Limits

- NEVER exceed 2 A5 pages
- NEVER use concepts not in `all_prior_concepts` + `concepts_new`
- NEVER skip supplementary annotations for concept-bearing scenario lines
- NEVER break character voice rules
- ALWAYS provide complete Key Concept Cards for all terms in `key_terms_new`

---

## Section E — HTML Assembly Instructions

### Base CSS Structure

Adapt from the A5 print-optimized CSS. Key specifications:

```css
@page {
  size: A5 portrait;
  margin: 15mm;
}

:root {
  /* Navy accent scale */
  --accent-deep:   #1a3a5c;
  --accent-accent:  #2a5a8c;
  --accent-mid:     #4a7ab0;
  --accent-soft:    #e8f0f8;
  --accent-ghost:   #f2f6fa;
  --accent-border:  #c8d8e8;

  /* Coral romantic accent */
  --coral-deep:    #c45a3c;
  --coral-accent:  #d4745a;
  --coral-soft:    #fdf0ec;
  --coral-border:  #e8c4b8;

  /* Neutrals */
  --ink:           #1a1a1a;
  --ink-light:     #4a4a4a;
  --rule:          #d0d0d0;
  --page:          #ffffff;
  --grey-100:      #f5f5f5;
  --grey-200:      #e8e8e8;
  --grey-300:      #d0d0d0;
}

body {
  font-family: 'Noto Sans', sans-serif;
  font-size: 9pt;
  line-height: 1.45;
  color: var(--ink);
  max-width: 118mm;
  margin: 0 auto;
}
```

### Character Color Classes

```css
.persona-ren    { background: #e3ecf5; color: #1a3a5c; }
.persona-saki   { background: #fdf0ec; color: #8c3a2a; }
.persona-tetsu  { background: #e8f5e8; color: #2a5c2a; }
.persona-kudo   { background: #f5f0e8; color: #5c4a1a; }
.persona-hina   { background: #f0e8f5; color: #4a2a5c; }
```

### Component CSS Classes

```css
/* Scenario */
.scenario { margin-bottom: 8px; }
.scene-setting { font-style: italic; color: var(--ink-light); margin-bottom: 4px; font-size: 8.5pt; }
.dialogue-line { margin-bottom: 3px; line-height: 1.5; }
.speaker-tag {
  display: inline-block;
  padding: 1px 6px;
  border-radius: 3px;
  font-weight: 600;
  font-size: 8pt;
  margin-right: 4px;
}
.annotation {
  font-size: 8pt;
  color: var(--ink-light);
  padding-left: 16px;
  margin-bottom: 4px;
  border-left: 2px solid var(--accent-border);
}

/* Concept Discovery Box */
.concept-box {
  background: var(--accent-ghost);
  border: 1px solid var(--accent-border);
  border-radius: 4px;
  padding: 8px 10px;
  margin-top: 8px;
  font-size: 8.5pt;
}
.concept-box-title {
  font-weight: 700;
  color: var(--accent-deep);
  margin-bottom: 4px;
  font-size: 9pt;
}
.concept-point { margin-bottom: 4px; }
.concept-point::before {
  content: attr(data-num);
  display: inline-block;
  width: 16px;
  height: 16px;
  background: var(--accent-accent);
  color: white;
  border-radius: 50%;
  text-align: center;
  font-size: 7pt;
  line-height: 16px;
  margin-right: 6px;
  font-weight: 700;
}

/* Key Concept Card */
.term-card {
  border: 1px solid var(--accent-border);
  border-radius: 4px;
  padding: 8px 10px;
  margin-bottom: 6px;
  font-size: 8.5pt;
}
.term-card-name {
  font-weight: 700;
  color: var(--accent-deep);
  font-size: 9pt;
  border-bottom: 1px solid var(--accent-border);
  padding-bottom: 3px;
  margin-bottom: 4px;
}
.term-card-row { margin-bottom: 2px; }
.term-card-label {
  font-weight: 600;
  color: var(--accent-accent);
  font-size: 7.5pt;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

/* Reference Material */
.reference-material {
  font-family: 'Noto Serif', serif;
  font-size: 9pt;
  background: var(--grey-100);
  border-left: 3px solid var(--accent-mid);
  padding: 8px 10px;
  margin-bottom: 8px;
}
.reference-type-badge {
  display: inline-block;
  background: var(--accent-soft);
  color: var(--accent-deep);
  padding: 1px 8px;
  border-radius: 3px;
  font-family: 'Noto Sans', sans-serif;
  font-size: 7.5pt;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  margin-bottom: 4px;
}

/* Review Corner */
.review-corner {
  border-top: 1px solid var(--rule);
  padding-top: 8px;
  margin-top: 8px;
}
.review-title {
  font-weight: 700;
  color: var(--accent-deep);
  font-size: 9pt;
  margin-bottom: 6px;
}
.review-item { margin-bottom: 6px; }
.review-number {
  display: inline-block;
  width: 16px;
  height: 16px;
  background: var(--accent-accent);
  color: white;
  border-radius: 50%;
  text-align: center;
  font-size: 7pt;
  line-height: 16px;
  font-weight: 700;
  margin-right: 4px;
}
.review-annotation {
  font-size: 8pt;
  color: var(--ink-light);
  padding-left: 16px;
  border-left: 2px solid var(--coral-border);
  margin-top: 2px;
}

/* Romantic subplot moments — use coral accents */
.subplot-moment {
  border-left: 2px solid var(--coral-border);
  padding-left: 8px;
  margin: 4px 0;
}

/* Header */
.unit-header {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  border-bottom: 2px solid var(--accent-deep);
  padding-bottom: 4px;
  margin-bottom: 8px;
}
.unit-number {
  font-size: 7.5pt;
  font-weight: 700;
  color: var(--accent-accent);
  text-transform: uppercase;
  letter-spacing: 1px;
}
.unit-title {
  font-size: 11pt;
  font-weight: 700;
  color: var(--accent-deep);
}
.unit-subtitle {
  font-size: 8pt;
  color: var(--ink-light);
}

/* Footer */
.unit-footer {
  border-top: 1px solid var(--rule);
  padding-top: 4px;
  margin-top: 8px;
  font-size: 7pt;
  color: var(--grey-300);
  display: flex;
  justify-content: space-between;
}
```

### Section Assembly Order by Pattern

**Pattern A:**
1. Unit header (number, title, subtitle)
2. Scenario section (.scenario)
3. Concept Discovery Box (.concept-box)
4. Unit footer (series name, phase, page)

**Pattern B:**
1. Unit header
2. Reference Material (.reference-material) with type badge
3. Key Concept Cards (.term-card) — one per term
4. Unit footer

**Pattern C:**
1. Unit header
2. Scenario section (.scenario) — shorter than Pattern A
3. Key Concept Cards (.term-card)
4. Review Corner (.review-corner)
5. Unit footer

### HTML Skeleton

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Project Doki Doki — Unit {XX}: {scene_title}</title>
  <style>
    /* === Full CSS from above === */
  </style>
</head>
<body>
  <header class="unit-header">
    <div>
      <span class="unit-number">Unit {XX} · Phase {N}</span>
      <h1 class="unit-title">{scene_title}</h1>
      <p class="unit-subtitle">{scene_title_sub}</p>
    </div>
  </header>

  <!-- Pattern-specific sections go here -->

  <footer class="unit-footer">
    <span>Project Doki Doki</span>
    <span>Phase {N} · Unit {XX} / 100</span>
  </footer>
</body>
</html>
```

### Write Output

- File path: `./export/HTML/unit_XX.html` (zero-padded to 2 digits: `unit_01.html`, `unit_99.html`, `unit_100.html`)
- After writing, increment the value in `./current_index.txt` by 1

---

## Section F — Pre-Write Validation Checklist

Before writing the HTML file, verify ALL of the following:

- [ ] Every PM term either (a) is in `all_prior_terms` or (b) has an inline gloss in parentheses
- [ ] Every concept used is in `all_prior_concepts` or is being introduced in `concepts_new`
- [ ] All items in `concepts_new` appear in the scenario at least once each
- [ ] Character dialogue matches their voice profiles (Section A)
- [ ] Supplementary annotations are present for all concept-bearing scenario lines
- [ ] All terms in `key_terms_new` have complete Key Concept Cards
- [ ] HTML is valid and self-contained (no external dependencies except Google Fonts)
- [ ] File path is correctly zero-padded (`unit_01.html` not `unit_1.html`)
- [ ] `current_index.txt` will be incremented after write
- [ ] `narrative_subplot` beat is reflected in the scenario (if non-empty)
- [ ] Page count does not exceed 2 A5 pages (use heuristics from Section A)
- [ ] Review Corner mini-scenarios (Pattern C) use NEW situations, not repeated old scenes
- [ ] Review Corner references concepts from `review_source` units
- [ ] Reference material (Pattern B) matches `reference_type` and `reference_topic`
- [ ] No character appears in dialogue who is not listed in the `characters` column
