# K9 Architect — Design System

## Overview

**K9 Architect** is a web application for designing, running, tracking and documenting individualised canine behaviour-modification programmes. It combines a planning engine built on applied behaviour analysis principles, structured session tracking, retrieval over a specialist corpus, and a connected experience shared by owners and professionals.

The product is a **single-surface technical dashboard** — a web application used by two linked roles: the **professional** who manages clients, cases and sessions, and the **owner** who works with their dog and reports what happened. Think of it as a case and progression system, not a consumer training app.

> ⚠️ **Read before writing any copy in this system.**
> K9 operates under a strict claims regime. Product surfaces, marketing and documentation must all say the same thing, and several intuitive phrasings are forbidden. See **[Claims-safe language](#claims-safe-language)** below, and the authoritative registers:
> - [`docs/product/RELEASE-READINESS-AND-CLAIMS.md`](../docs/product/RELEASE-READINESS-AND-CLAIMS.md) — what may be claimed, per capability
> - [`docs/product/PRODUCT-REFERENCE.md`](../docs/product/PRODUCT-REFERENCE.md) — what the product actually does

### Sources

- `uploads/DD-new_design_K9.md` — original design directive: typography, colours, UI element rules, dark/light specs, per-screen prompts.
- `colors_and_type.css` — **source of truth for all colour and type tokens.** Where this README and the CSS disagree, the CSS wins.
- No Figma link or repo was provided; this design system is built from the directive above plus the shipped token file.

---

## Products

| Surface | Description |
|---|---|
| **App (dashboard)** | Web application with sidebar navigation, dog and case management, session reports, step-based behaviour programmes, an attention panel, PDF reports, and a scoped AI query interface |

UI kit at: `ui_kits/app/`

---

## Claims-safe language

This section is **binding**, not stylistic. It exists because the same words that feel natural in this category are the ones that create legal and product risk.

### Forbidden vocabulary

Never use these in UI labels, empty states, tooltips, error messages, onboarding copy, marketing or documentation:

| Forbidden | Use instead | Why |
|---|---|---|
| clinical, clinic, patient, treatment, therapy | behavioural, case, programme, session | Raises regulatory and legal exposure |
| diagnosis, diagnose | **working hypothesis**, functional hypothesis | The product does not diagnose |
| homework | **reported practice**, session | No homework subsystem with due dates or reminders exists |
| cure, fix, eliminate the behaviour, guaranteed | *(no equivalent — do not claim outcomes)* | No outcome may be promised |
| scientifically proven, evidence-based, validated | **specialist corpus**, shows available sources | Retrieval is fail-soft; sources are shown, not proven |
| with your logo | **with your business name** | Reports carry a text business name only |
| download the app, available on iOS/Android | **web application** | No published store build exists |
| 80% or more, ≥ 80% | **above 80%** | The implemented threshold is strictly `> 0.8` |
| health tracking, health status | *(not a product capability)* | Not implemented; do not surface it |
| kennel, kennels | **owners**, dogs, cases | Renamed. See `CLAUDE.md` |

### Rules for AI-related copy

- **The AI is a mechanism, never the promise.** Do not label anything "AI-powered". Describe what it does.
- **No first-person AI voice.** Never "I think", "I found", "I decided". Results are presented factually.
- **The professional keeps judgement.** No string may imply the system decides on its own. It structures, records and can refuse; a person decides.
- The AI query surface is **scoped**: it answers from the corpus, shows available sources, does not modify the plan, and can stop and refer instead of answering.
- In the EU, an AI interaction must be identifiable as such. Where required, surface the disclosure string agreed with legal review.

### Rules for outcome copy

- Certainty is about **process**, never about the dog.
- A safeguard is never a guarantee. Write "can pause or refer", not "keeps your dog safe".
- Progression states are **criteria**, not victories. `Criterion met` — never "Success!" or "Great job!".
- No timeframes. No before/after. No success rates — the product has none.

### Status and semantics

Colour carries meaning in this system and that meaning is fixed:

| Token | Means | Does **not** mean |
|---|---|---|
| Red `#ef4444` | Action, brand, pause | Danger, alarm |
| Green `#10b981` | **Criterion met** | The dog succeeded, celebration |
| Amber `#f59e0b` | Attention, observe, review | Dramatic warning |

**Meaning is never carried by colour alone.** Every state that uses colour also carries a word.

### Demonstration data

Any screenshot, prototype, marketing still or video frame showing the interface must carry a visible `DEMONSTRATION DATA` label and must contain no real personal data.

---

## CONTENT FUNDAMENTALS

### Voice & tone

- **Professional, precise, observational.** A tool for people who work with behaviour — not a consumer pet app. Copy should read like well-designed technical software.
- **Terse and functional.** Labels are short and action-oriented. No fluff, no exclamation marks.
- **Behavioural vocabulary is expected.** Terms like "desensitisation", "counterconditioning", "reinforcement schedule" and "threshold" are used without explanation on professional surfaces. On owner surfaces, plain language and one actionable idea at a time.
- **Two audiences, one product.** Professional surfaces assume expertise. Owner surfaces assume none. Neither is ever set against the other.
- **No emoji** in UI. Status is communicated through colour-coded badges plus text.
- **Describe observable behaviour.** Never attribute intent to a dog as if it were fact.

### Casing

| Context | Convention |
|---|---|
| Navigation items, section headers, card titles | **Title Case** *(product UI only)* |
| Body text, descriptions, table values | Sentence case |
| Status badges | ALL CAPS, monospace |
| Case IDs, dog tags, session IDs | Monospace, uppercase |
| **Marketing headlines, advertising, OOH** | **Sentence case — always** |

> **Note.** Product UI casing and marketing casing are deliberately different conventions and this is the one open point between this document and the brand platform. Product UI currently uses Title Case for navigation; all outward-facing communication uses sentence case. If the two are to be unified, that is an Art Direction decision — until then, do not "correct" one to match the other.

### Language

- **Product surfaces ship Spanish-first** for the Spanish market. The public Library carries Spanish and English where a translation exists; a visible fallback is kept where it does not.
- **This design-system documentation is written in English** for tooling reasons. That is a documentation convention, not a product language decision.
- English UI strings used in kits and prototypes are placeholders unless a localisation decision says otherwise.

### Example copy patterns

- `CRITERION MET` / `ATTENTION` / `PAUSED` / `READ-ONLY` — status badges
- "Behaviour programme" / "Session report" / "Case overview" — section headers
- "Save" / "Refresh" / "Generate report" — action buttons
- "Reported practice" / "Attention panel" / "Library" — nav labels
- "Reduce one dimension" / "Repeat to consolidate" / "Above 80%" — progression decisions

---

## VISUAL FOUNDATIONS

### Colour system

**`colors_and_type.css` is the source of truth.** The table below reflects it; if it ever drifts, the CSS wins.

| Role | Hex | Usage |
|---|---|---|
| **Primary Red** | `#ef4444` | Brand — active nav, primary buttons, selected states, the `9` in the wordmark |
| **Success Green** | `#10b981` | Criterion met, active toggles |
| **Warning Orange** | `#f59e0b` | Attention states, review needed |
| **Dark BG (page)** | `#1a1b1e` | Dark mode page background |
| **Dark BG (card)** | `#25262b` | Dark mode card/panel background |
| **Dark border** | `#373a40` | Dark mode card borders |
| **Light BG (page)** | `#f3f4f6` | Light mode page background |
| **Light BG (card)** | `#fefefe` | Light mode card/panel background |
| **Light border** | `#e2e3e4` | Light mode card borders |

Text neutrals: `#f1f2f4` primary · `#c1c2c5` secondary · `#909399` muted · `#636670` disabled.

**Blue, teal and purple** appear as card-overlay values in `CLAUDE.md` but are **not defined as primitives** in `colors_and_type.css`. They are not part of the brand palette and must not be used in outward-facing communication. Either add them as tokens or stop referencing them.

### Typography

| Role | Font | Usage |
|---|---|---|
| **Body / UI** | Space Grotesk | Body text, sidebar labels, nav, paragraphs, general UI labels |
| **Data / dense** | JetBrains Mono | Small headers, calendar days, data grids, status badges, IDs, dates, criteria |

The governing idea: **Space Grotesk is the voice of the brand; JetBrains Mono is the voice of the system.** A headline in mono reads as machine output; a datum in Space Grotesk loses its record-like texture. Keep the two roles separate.

Both fonts are available locally in `fonts/` and declared in `colors_and_type.css`.

### Spacing & radius

- **Corner radius:** `8px` on all cards, containers, panels
- **Borders:** `1px` solid, subtle, using the border tokens
- **Sidebar width:** ~190–240px
- **Card padding:** `16–24px`

### Backgrounds & depth

- Two-level depth: page background is darker than card background in both modes.
- No full-bleed background images or illustrations.
- No gradients on backgrounds. Clean flat surfaces.
- Very subtle low-elevation `box-shadow` may be used on cards.

### Brand mark

The identity is a **wordmark with no glyph**. `K` in primary text colour, `9` in Primary Red, followed by "Architect".

Two lockups are under evaluation (`assets/K9 Architect logo options/`):

- **1A · inline, weight contrast** — `K9` bold, `Architect` light, on one baseline.
- **1B · stacked, mono baseline** — `K9` bold above `ARCHITECT` in JetBrains Mono with wide tracking.

The square mark for app icon, favicon and avatar is **type only**: `K9` in a rounded square.

**Forbidden in any mark, icon or illustration:** paw prints, dog faces, breed silhouettes, dogs inside shields, police or tactical styling, brains with circuitry, robots, AI sparkles, chat bubbles.

**One logo for both audiences.** There is no separate professional mark.

### Sidebar navigation

- Left sidebar: icon + text.
- Active item: red text on `rgba(239,68,68,0.1)` background tint.
- Inactive: muted grey text, no background.
- Icons: minimalist stroke icons.

### Badges & status indicators

- **Pill-shaped** with a small coloured dot.
- Text uppercase, monospace.
- Green (criterion met), amber (attention), red (paused/action), grey (inactive).
- Always paired with a word — never colour alone.

### Buttons

- **Primary:** red `#ef4444` background, white text, `8px` radius.
- **Secondary / outline:** transparent background, grey text, subtle grey border; hover changes border and text colour.
- **Destructive:** red outline or red fill depending on context.

### Toggles

- Minimalist pill toggle.
- **Active:** green `#10b981` track, white knob.
- **Inactive:** grey track, white knob.

### Coloured card variant

**Never use a thick left or top accent border.** Use a uniform 1px border at 35% opacity with a 7% background overlay. Full reference in `CLAUDE.md`.

### Animation & interactions

- Minimal, functional transitions only, ~150ms ease.
- Animate `transform` and `opacity`. Do not animate layout.
- No bouncy or playful motion.
- **Nothing may suggest the AI is "thinking"**: no particles, no pulses, no scanning sweeps.
- Data appears; it does not count up like a scoreboard.

### Dark vs light mode

- Dark mode is the **primary** mode — this is a technical dashboard.
- Light mode is fully supported.
- Cards always float above the page background in both modes.
- **Note for print and outdoor:** the dark system is for emissive and backlit surfaces. Printed, reflected media use the light system. See the outdoor guidance in [`docs/marketing/briefing-agencias/05-exterior-y-grafica-estatica.md`](../docs/marketing/briefing-agencias/05-exterior-y-grafica-estatica.md).

### Imagery

- No decorative photography or illustration inside the product.
- Data-driven visualisation — charts, grids, calendars — is the main "imagery".
- Data-viz colour uses the brand semantic palette and respects its meanings.

---

## ICONOGRAPHY

### Approach

- **Minimalist stroke icons**, Lucide or equivalent, 1.5px stroke, 24px default and 16px in dense areas.
- SVG only. No icon font. No emoji. No filled or gradient icons.
- Icons appear in sidebar navigation, button prefixes and table actions. Status badges use a dot, not an icon.

### Icon system: Lucide

- CDN: `https://unpkg.com/lucide@latest/dist/umd/lucide.min.js`
- Usage: `<i data-lucide="dog"></i>` with `lucide.createIcons()`
- Size: 18–20px sidebar, 14–16px inline

### Key icons

| Context | Icon |
|---|---|
| Dogs | `dog` |
| Owners / clients | `users`, `user` |
| Sessions / calendar | `calendar`, `clock` |
| Programmes / steps | `list-checks`, `git-branch` |
| Attention / welfare | `alert-triangle`, `activity` |
| Settings | `settings` |
| AI query | `search`, `message-square-text` |
| Reports | `file-text`, `bar-chart-2` |
| Library | `book-open` |

**Removed deliberately:** `paw-print` — the identity is glyph-free and explicitly avoids paw imagery. `brain` and `bot` — the AI is a mechanism, not a character.

---

## File index

```
README.md                     — This file; design system guide
CLAUDE.md                     — Project rules: card variants, theme, naming
SKILL.md                      — Agent skill definition
colors_and_type.css           — SOURCE OF TRUTH for colour, type, spacing, radius
fonts/                        — Space Grotesk + JetBrains Mono (local)
assets/
  K9 Architect logo options/  — Wordmark lockups under evaluation (1A, 1B)
proposals/
  k9-architect/               — Earlier identity exploration (monogram); superseded
preview/                      — Design system tab cards (registered HTML previews)
  brand-logo.html             — ⚠️ still shows the retired paw mark; needs updating
  colors-primary.html         — Primary colour palette
  colors-semantic.html        — Semantic / state colours
  colors-dark.html            — Dark mode surface tokens
  colors-light.html           — Light mode surface tokens
  type-scale.html             — Typography scale (Space Grotesk)
  type-mono.html              — Monospace type (JetBrains Mono)
  spacing-radius.html         — Spacing, radius, borders
  components-buttons.html     — Button variants
  components-badges.html      — Status badge variants
  components-toggles.html     — Toggle switches
  components-sidebar.html     — Sidebar navigation
  components-cards.html       — Card containers
  components-inputs.html      — Form inputs
  components-focus-ring.html  — Focus / active border token
plantillas-carrusel/          — Carousel templates (dark + light)
library-post-spec.md          — Library post specification
ui_kits/
  app/                        — App dashboard prototype and components
```

---

## Known inconsistencies

Tracked here so they are fixed rather than propagated.

| # | Issue | Status |
|---|---|---|
| 1 | `preview/brand-logo.html` still renders the retired paw mark | **Open** — update to the approved wordmark |
| 2 | `ui_kits/app/` prototype uses `Kennel Overview`, `Session Log`, `Protocol Library` | **Open** — rename to owner/case vocabulary |
| 3 | Blue, teal and purple documented in `CLAUDE.md` but absent from `colors_and_type.css` | **Open** — add as tokens or remove the reference |
| 4 | Product UI Title Case vs marketing sentence case | **Open** — Art Direction decision |
| 5 | Wordmark lockup 1A vs 1B | **Open** — client decision |
