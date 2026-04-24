# STYLE_GUIDELINE.md — Visual Design for Project Doki Doki

---

## Color Palette

### Primary Accent — Navy (Professional / Structure)

The navy palette represents the PM discipline side of the series: frameworks, processes, and rigor.

| Token | Hex | Usage |
|-------|-----|-------|
| `--accent-deep` | `#1a3a5c` | Headings, unit title, primary emphasis |
| `--accent-accent` | `#2a5a8c` | Labels, term card names, numbered badges, bold callouts |
| `--accent-mid` | `#4a7ab0` | Reference material left border, divider accents |
| `--accent-soft` | `#e8f0f8` | Reference type badge background, example highlights |
| `--accent-ghost` | `#f2f6fa` | Concept Discovery Box background fill |
| `--accent-border` | `#c8d8e8` | Concept box border, term card border, annotation left border |

### Secondary Accent — Coral (Romantic / Emotional)

The coral palette surfaces during subplot moments and emotional beats.

| Token | Hex | Usage |
|-------|-----|-------|
| `--coral-deep` | `#c45a3c` | Subplot moment emphasis (sparingly) |
| `--coral-accent` | `#d4745a` | Romantic beat callouts |
| `--coral-soft` | `#fdf0ec` | Saki's persona tag background, subplot moment background |
| `--coral-border` | `#e8c4b8` | Review annotation left border, subplot moment left border |

### Neutrals

| Token | Hex | Usage |
|-------|-----|-------|
| `--ink` | `#1a1a1a` | Body text, primary content |
| `--ink-light` | `#4a4a4a` | Annotations, subtitles, scene-setting text |
| `--rule` | `#d0d0d0` | Hairline dividers between sections |
| `--page` | `#ffffff` | Page background |
| `--grey-100` | `#f5f5f5` | Reference material background |
| `--grey-200` | `#e8e8e8` | Inactive elements, secondary backgrounds |
| `--grey-300` | `#d0d0d0` | Footer text, muted labels |

### Character Colors

Desaturated pastels — each character gets a distinct but soft identity color.

| Character | Background | Text | CSS Class |
|-----------|-----------|------|-----------|
| Ren (蓮) | `#e3ecf5` | `#1a3a5c` | `.persona-ren` |
| Saki (咲希) | `#fdf0ec` | `#8c3a2a` | `.persona-saki` |
| Tetsu (哲) | `#e8f5e8` | `#2a5c2a` | `.persona-tetsu` |
| Director Kudo (工藤部長) | `#f5f0e8` | `#5c4a1a` | `.persona-kudo` |
| Hina (陽菜) | `#f0e8f5` | `#4a2a5c` | `.persona-hina` |

---

## Typography

### Font Stack

| Context | Font | Fallback |
|---------|------|----------|
| Body text, headings, UI elements | Noto Sans | Helvetica Neue, Arial, sans-serif |
| Reference material sections | Noto Serif | Georgia, Times New Roman, serif |

Load via Google Fonts:
```html
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans:wght@400;600;700&family=Noto+Serif:wght@400;700&display=swap" rel="stylesheet">
```

### Type Scale

| Element | Font | Size | Weight | Color |
|---------|------|------|--------|-------|
| Unit title | Noto Sans | 11pt | 700 | `--accent-deep` |
| Unit number label | Noto Sans | 7.5pt | 700 | `--accent-accent` |
| Subtitle | Noto Sans | 8pt | 400 | `--ink-light` |
| Body text | Noto Sans | 9pt | 400 | `--ink` |
| Scenario dialogue | Noto Sans | 9pt | 400 | `--ink` |
| Scene-setting text | Noto Sans | 8.5pt | 400 italic | `--ink-light` |
| Speaker tag | Noto Sans | 8pt | 600 | per character |
| Annotation text | Noto Sans | 8pt | 400 | `--ink-light` |
| Concept box title | Noto Sans | 9pt | 700 | `--accent-deep` |
| Concept box body | Noto Sans | 8.5pt | 400 | `--ink` |
| Term card name | Noto Sans | 9pt | 700 | `--accent-deep` |
| Term card body | Noto Sans | 8.5pt | 400 | `--ink` |
| Term card label | Noto Sans | 7.5pt | 600 | `--accent-accent` |
| Reference material | Noto Serif | 9pt | 400 | `--ink` |
| Reference type badge | Noto Sans | 7.5pt | 600 | `--accent-deep` |
| Review corner title | Noto Sans | 9pt | 700 | `--accent-deep` |
| Review mini-scenario | Noto Sans | 8.5pt | 400 | `--ink` |
| Footer | Noto Sans | 7pt | 400 | `--grey-300` |

---

## Layout & Grid

### Page Setup

| Property | Value |
|----------|-------|
| Page size | A5 portrait (148 × 210mm) |
| Margins | 15mm all sides |
| Content width | 118mm |
| Pages per unit | 2 (strict maximum) |

### Vertical Rhythm

| Spacing Token | Value | Usage |
|---------------|-------|-------|
| `section-gap` | 8px | Between major sections (scenario → concept box, reference → term cards) |
| `paragraph-gap` | 4px | Between items within a section (between dialogue lines, between term cards) |
| `component-gap` | 6px | Between term cards, between review items |
| `inner-padding` | 8px 10px | Inside concept boxes, term cards |
| `annotation-indent` | 16px | Left padding for annotation text |

### Section Separation

Sections are separated by **hairline rules** (`1px solid var(--rule)`), not whitespace gaps. This maximizes content density within the 2-page constraint.

Exceptions:
- Concept Discovery Box uses a filled background + border instead of a rule
- Term cards use their own border instead of a dividing rule
- The unit header uses a `2px solid var(--accent-deep)` bottom border

---

## Component Catalog

### 1. Unit Header

```
┌─────────────────────────────────────────┐
│ UNIT 01 · PHASE 1                       │
│ The First Meeting                        │
│ Ren meets his new client — and her PM    │
└─────────────────────────────────────────┘
  2px solid accent-deep bottom border
```

- Unit number: uppercase, letter-spaced, `--accent-accent`
- Title: 11pt bold, `--accent-deep`
- Subtitle: 8pt regular, `--ink-light`

### 2. Persona Tag (Speaker Tag)

```
┌──────────┐
│ Ren (蓮) │  ← pill shape, persona background color
└──────────┘
```

- Inline-block pill with 3px border-radius
- Background and text color from character color table
- 8pt, 600 weight
- Followed by dialogue text on the same line

### 3. Scenario Section

```
Scene-setting text in italic (8.5pt, ink-light)

[Persona Tag] Dialogue line with **bold terms** and *italic frameworks*
  → Annotation: PM context explanation (8pt, ink-light, border-left)

[Persona Tag] Next dialogue line...
  → Annotation if needed
```

### 4. Concept Discovery Box

```
┌─ accent-border ─────────────────────────┐
│  ░░░ accent-ghost background ░░░░░░░░░  │
│                                          │
│  Concept Discovery                       │  ← 9pt bold, accent-deep
│                                          │
│  ① First concept explanation...          │  ← numbered badge (accent-accent circle)
│     "When Saki mentioned baseline..."    │
│                                          │
│  ② Second concept explanation...         │
│                                          │
└──────────────────────────────────────────┘
```

### 5. Key Concept Card (Term Card)

```
┌─ accent-border ─────────────────────────┐
│  STAKEHOLDER                             │  ← 9pt bold, accent-deep
│  ─────────────────── (hairline)          │
│  DEFINITION  An individual, group, or    │  ← label 7.5pt uppercase accent-accent
│  organization that may affect or be      │
│  affected by the project.                │
│  COMPONENTS  • Power/Interest level      │
│              • Engagement strategy       │
│              • Communication needs       │
│  RELATED  sponsor, project team, PMO     │
│  EXAMPLE  Director Kudo is a high-power  │
│  stakeholder who requires frequent       │
│  updates to maintain engagement.         │
└──────────────────────────────────────────┘
```

### 6. Reference Material Block

```
  ┌────────────────┐
  │ STATUS REPORT  │  ← reference type badge (accent-soft bg)
  └────────────────┘
  ┃                                        ┃
  ┃  Reference material body text          ┃  ← Noto Serif, 9pt
  ┃  in grey-100 background with           ┃     3px accent-mid left border
  ┃  accent-mid left border...             ┃
  ┃                                        ┃
```

### 7. Review Corner

```
  ──────────────── (hairline rule) ─────────

  Review Corner                            ← 9pt bold, accent-deep

  ① [Mini-scenario title]
     [Persona Tag] Dialogue line...
     [Persona Tag] Response line...
     → Review annotation (coral-border left)

  ② [Mini-scenario title]
     ...
```

### 8. Subplot Moment

When a dialogue line or moment carries romantic subplot weight, wrap it:

```
  ┃  [line with subplot significance]      ┃  ← coral-border left border
  ┃                                        ┃     2px solid coral-border
```

Use sparingly — 0–2 times per unit maximum. The coral accent should feel like a blush, not a spotlight.

### 9. Unit Footer

```
  ──────────────── (hairline rule) ─────────
  Project Doki Doki          Phase 1 · Unit 01 / 100
```

- 7pt, `--grey-300`
- Flex layout: series name left, phase/unit right

---

## Print Optimization

### CSS @page Rules

```css
@page {
  size: 148mm 210mm;   /* A5 portrait */
  margin: 15mm;
}

@media print {
  body {
    -webkit-print-color-adjust: exact;
    print-color-adjust: exact;
  }
  .unit-footer {
    position: fixed;
    bottom: 0;
  }
}
```

### Browser Print Settings (User Instructions)

1. Open HTML file in Chrome/Edge
2. File → Print (or Cmd+P)
3. Destination: Save as PDF
4. Paper size: A5
5. Margins: None (margins are built into the CSS)
6. Background graphics: ON (required for persona tags, concept boxes, term cards)
7. Scale: 100%

---

## Design Principles

1. **Density over whitespace.** Every square millimeter matters on A5. Use tight spacing, hairline rules, and compact components.
2. **Color as information.** Navy = PM structure. Coral = emotional beat. Character colors = who's speaking. Never decorative.
3. **Serif for artifacts, sans for everything else.** When the learner sees Noto Serif, they know they're reading a "real document" (reference material). Noto Sans means they're in the learning frame.
4. **Progressive familiarity.** The visual system is identical across all 100 units. The learner's eye should know exactly where to look by unit 5.
5. **Print-first.** Every design decision optimizes for A5 paper output. Screen rendering is secondary.
