---
name: design-taste-frontend
description: Anti-slop frontend skill for landing pages, portfolios, and redesigns. The agent reads the brief, infers the right design direction, and ships interfaces that do not look templated. Real design systems when applicable, audit-first on redesigns, strict pre-flight check.
---

# tasteskill: Anti-Slop Frontend Skill

> Landing pages, portfolios, and redesigns. Not dashboards, not data tables, not multi-step product UI.
> Every rule below is **contextual**. None of it fires automatically. First read the brief, then pull only what fits.

---

## 0. BRIEF INFERENCE (Read the Room Before Anything Else)

Before touching code or tweaking dials, **infer what the user actually wants**. Most LLM design output is bad because the model jumps to a default aesthetic instead of reading the room.

### 0.A Read these signals first
1. **Page kind** - landing (SaaS / consumer / agency / event), portfolio (dev / designer / creative studio), redesign (preserve vs overhaul), editorial / blog.
2. **Vibe words** the user used - "minimalist", "calm", "Linear-style", "Awwwards", "brutalist", "premium consumer", "Apple-y", "playful", "serious B2B", "editorial", "agency-y", "glassy", "dark tech".
3. **Reference signals** - URLs they linked, screenshots they pasted, products they named, brands they're competing with.
4. **Audience** - B2B procurement panel vs. design-conscious consumer vs. recruiter scanning a portfolio.
5. **Brand assets that already exist** - logo, color, type, photography.
6. **Quiet constraints** - accessibility-first audiences, public-sector, regulated industries, trust-first commerce, kids' products.

### 0.B Output a one-line "Design Read" before generating
Before any code, state in one line: **"Reading this as: <page kind> for <audience>, with a <vibe> language, leaning toward <design system or aesthetic family>."**

### 0.C If the brief is ambiguous, ask one question, do not guess
### 0.D Anti-Default Discipline
Do not default to: AI-purple gradients, centered hero over dark mesh, three equal feature cards, generic glassmorphism, Inter + slate-900.

---

## 1. THE THREE DIALS

* **DESIGN_VARIANCE: 8** - 1 = Perfect Symmetry, 10 = Artsy Chaos
* **MOTION_INTENSITY: 6** - 1 = Static, 10 = Cinematic / Physics
* **VISUAL_DENSITY: 4** - 1 = Art Gallery / Airy, 10 = Cockpit / Packed Data

**Baseline:** `8 / 6 / 4`.

### 1.A Dial Inference
| Signal | VARIANCE | MOTION | DENSITY |
|---|---|---|---|
| "minimalist / clean / calm / editorial / Linear-style" | 5-6 | 3-4 | 2-3 |
| "premium consumer / Apple-y / luxury / brand" | 7-8 | 5-7 | 3-4 |
| "playful / wild / Dribbble / Awwwards / experimental / agency" | 9-10 | 8-10 | 3-4 |
| "landing page / portfolio / marketing site (default)" | 7-9 | 6-8 | 3-5 |
| "trust-first / public-sector / regulated / accessibility-critical" | 3-4 | 2-3 | 4-5 |

### 1.B Use-Case Presets
| Use case | VARIANCE | MOTION | DENSITY |
|---|---|---|---|
| Landing (SaaS, mainstream) | 7 | 6 | 4 |
| Landing (Agency / creative) | 9 | 8 | 3 |
| Landing (Premium consumer) | 7 | 6 | 3 |
| Portfolio (Designer / studio) | 8 | 7 | 3 |
| Portfolio (Developer) | 6 | 5 | 4 |
| Editorial / Blog | 6 | 4 | 3 |
| Public-sector service | 3 | 2 | 5 |

---

## 2. BRIEF → DESIGN SYSTEM MAP

### 2.A When to reach for a real design system (use official packages)
| Brief reads as... | Reach for |
|---|---|
| Microsoft / enterprise SaaS / dashboards | `@fluentui/react-components` |
| Google-ish UI, Material-flavored product | `@material/web` |
| IBM-style B2B / enterprise analytics | `@carbon/react` |
| Shopify app surfaces | `polaris.js` |
| Atlassian / Jira-style product | `@atlaskit/*` |
| GitHub-style devtool / community page | `@primer/css` |
| Public-sector UK service | `govuk-frontend` |
| Modern accessible React foundation | `@radix-ui/themes` |
| Modern SaaS where you own the components | shadcn/ui |
| Tailwind-based modern SaaS / AI marketing | Tailwind v4 |

**Honesty rule:** if the brief reads as one of the systems above, install and use the **official** package.
**One system per project.**

### 2.B When the brief is an aesthetic, not a system
Build with native CSS + Tailwind + a maintained component library. Be honest about borrowed inspiration.

| Aesthetic | Honest implementation |
|---|---|
| Glassmorphism / "frosted glass" | `backdrop-filter`, layered borders. Solid-fill fallback. |
| Bento (Apple-style tile grids) | CSS Grid with mixed cell sizes. |
| Brutalism | Native CSS, monospace, raw borders. |
| Editorial / magazine | Serif type, asymmetric grid, generous whitespace. |
| Dark tech / hacker | Mono + accent neon, terminal motifs. |
| **Apple Liquid Glass** | Web approximation only. No official `liquid-glass.css`. |

---

## 3. DEFAULT ARCHITECTURE & CONVENTIONS

### 3.A Stack
* **Framework:** React or Next.js. Default to Server Components (RSC).
* **Styling:** **Tailwind v4** (default). Tailwind v3 only if existing project demands it.
* **Animation:** **Motion** (`import { motion } from "motion/react"`).
* **Fonts:** Always use `next/font` or self-host with `@font-face` + `font-display: swap`.

### 3.B State
* Local `useState` / `useReducer` for isolated UI.
* Global state ONLY for deep prop-drilling avoidance - Zustand, Jotai, or React context.
* **NEVER** use `useState` for continuous values driven by user input. Use Motion's `useMotionValue` / `useTransform` / `useScroll`.

### 3.C Icons
* **Allowed libraries (priority order):** `@phosphor-icons/react`, `hugeicons-react`, `@radix-ui/react-icons`, `@tabler/icons-react`.
* **Discouraged:** `lucide-react`.
* **NEVER hand-roll SVG icons.**
* **One family per project.**
* **Standardize `strokeWidth` globally** (e.g. `1.5` or `2.0`).

### 3.D Emoji Policy
Discouraged by default in code, markup, and visible text.

### 3.E Responsiveness & Layout Mechanics
* Standardize breakpoints (`sm 640`, `md 768`, `lg 1024`, `xl 1280`, `2xl 1536`).
* **Viewport Stability:** NEVER use `h-screen` for full-height Hero sections. ALWAYS use `min-h-[100dvh]`.
* **Grid over Flex-Math:** NEVER use complex flexbox percentage math. ALWAYS use CSS Grid.

### 3.F Dependency Verification (mandatory)
Before importing ANY 3rd-party library, check `package.json`.

---

## 4. DESIGN ENGINEERING DIRECTIVES (Bias Correction)

### 4.1 Typography
* **Display / Headlines:** Default `text-4xl md:text-6xl tracking-tighter leading-none`.
* **Body / Paragraphs:** Default `text-base text-gray-600 leading-relaxed max-w-[65ch]`.
* **Sans font choice:** Discouraged as default: `Inter`. Pick `Geist`, `Outfit`, `Cabinet Grotesk`, `Satoshi` first.
* **SERIF DISCIPLINE:** Serif is very discouraged as default. Only when brand explicitly names a serif font or truly editorial/luxury.
* **Specifically BANNED as defaults:** `Fraunces` and `Instrument_Serif`.
* **ITALIC DESCENDER CLEARANCE (mandatory):** When italic is used in display type with descender letters, use `leading-[1.1]` minimum + `pb-1` reserve.

### 4.2 Color Calibration
* Max 1 accent color. Saturation < 80% by default.
* **THE LILA RULE:** The "AI Purple / Blue glow" aesthetic is discouraged as default.
* **One palette per project.**
* **COLOR CONSISTENCY LOCK (mandatory):** Once an accent color is chosen, used on WHOLE page.

### 4.3 Layout Diversification
* **ANTI-CENTER BIAS:** Centered Hero / H1 avoided when `DESIGN_VARIANCE > 4`.
* **Override:** centered hero OK for editorial / manifesto / launch-announcement briefs.

### 4.4 Materiality, Shadows, Cards
* Use cards ONLY when elevation communicates real hierarchy.
* When a shadow is used, tint it to the background hue.
* **SHAPE CONSISTENCY LOCK (mandatory):** Pick ONE corner-radius scale for the page.

### 4.5 Interactive UI States
* **Loading:** Skeletal loaders matching the final layout's shape.
* **Empty States:** Beautifully composed.
* **Error States:** Clear, inline or contextual.
* **Tactile Feedback:** On `:active`, use `-translate-y-[1px]` or `scale-[0.98]`.
* **BUTTON CONTRAST CHECK (mandatory, a11y):** WCAG AA min (4.5:1 for body, 3:1 for large text).
* **CTA BUTTON WRAP BAN (mandatory):** Button text MUST fit on one line at desktop.
* **NO DUPLICATE CTA INTENT (mandatory):** One label per intent per page.
* **FORM CONTRAST CHECK (mandatory, a11y):** All form elements pass WCAG AA contrast.

### 4.6 Data & Form Patterns
* Label ABOVE input. No placeholder-as-label.

### 4.7 Layout Discipline (Hard Rules)
* **Hero MUST fit in the initial viewport.** Headline max 2 lines, subtext max 20 words AND max 3-4 lines.
* **HERO TOP PADDING CAP:** max `pt-24` at desktop.
* **HERO STACK DISCIPLINE (max 4 text elements):** eyebrow OR brand strip, headline, subtext, CTAs.
* **Navigation MUST render on a single line on desktop.** Height cap: 80px max.
* **Bento grids MUST have rhythm.** Vary composition.
* **BENTO CELL COUNT RULE:** N items → N cells.
* **Section-Layout-Repetition Ban.** Each layout family max ONCE per page.
* **ZIGZAG ALTERNATION CAP:** Max 2 consecutive image+text-split sections.
* **EYEBROW RESTRAINT:** Maximum 1 eyebrow per 3 sections.
* **SPLIT-HEADER BAN:** "left big headline + right small explainer paragraph" pattern banned as default.

### 4.8 Image & Visual Asset Strategy
1. Image-generation tool first.
2. Real web images second (`https://picsum.photos/seed/{descriptive-seed}/{w}/{h}`).
3. Last resort: labeled placeholder slots.
**Div-based fake screenshots are banned.**

### 4.9 Content Density
* Default content shape per section: short headline (≤ 8 words) + short sub-paragraph (≤ 25 words).
* No data-dump sections.
* Long lists (>5 items) need different UI components: 2-column split, card grid, tabs/accordion, horizontal scroll-snap.

### 4.10 Quotes & Testimonials
* Max 3 lines of quote body.
* Attribution: name + role + (optionally) company.

### 4.11 Page Theme Lock
The page has ONE theme. Sections do not invert.

---

## 5. CONTEXT-AWARE PROACTIVITY

* **Liquid Glass / Glassmorphism:** Appropriate for premium consumer, Apple-adjacent, luxury brand.
* **Magnetic Micro-physics:** Use when `MOTION_INTENSITY > 5` AND brief reads premium / playful / agency.
* **Perpetual Micro-Interactions:** Use when `MOTION_INTENSITY > 5` AND section actively benefits from motion.
* **"Motion claimed, motion shown."** If `MOTION_INTENSITY > 4`, page must actually move.
* **MOTION MUST BE MOTIVATED:** Each animation needs a reason.
* **MARQUEE MAX-ONE-PER-PAGE.**
* **GSAP Sticky-Stack** and **Horizontal-Pan** patterns with canonical skeletons.

## 6. PERFORMANCE & ACCESSIBILITY GUARDRAILS

* Animate ONLY `transform` and `opacity`.
* **Any motion above `MOTION_INTENSITY > 3` MUST honor `prefers-reduced-motion`.**
* **Dark Mode (mandatory for any consumer-facing page).**
* **Core Web Vitals Targets:** LCP < 2.5s, INP < 200ms, CLS < 0.1.
* Grain/noise filters EXCLUSIVELY on fixed, `pointer-events-none` pseudo-elements.

## 7. DIAL DEFINITIONS (Technical Reference)

### DESIGN_VARIANCE
* **1-3:** Symmetrical CSS Grid, equal paddings, centered alignment.
* **4-7:** Overlaps, varied aspect ratios, left-aligned headers.
* **8-10:** Masonry, fractional grid units, massive empty zones.
* **MOBILE OVERRIDE:** Levels 4-10 collapse to single-column on `< 768px`.

### MOTION_INTENSITY
* **1-3:** No automatic animations. CSS `:hover` and `:active` only.
* **4-7:** `transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1)`.
* **8-10:** Complex scroll-triggered reveals, parallax. **NEVER `window.addEventListener('scroll')`.**

### VISUAL_DENSITY
* **1-3:** Lots of white space, `py-32` to `py-48`.
* **4-7:** Standard web app spacing `py-16` to `py-24`.
* **8-10:** Tight paddings, 1px lines, `font-mono` for all numbers.

## 8. DARK MODE PROTOCOL

Dual-mode by default. Pick one token strategy per project.

## 9. AI TELLS (Forbidden Patterns)

### 9.A Visual & CSS
* NO neon / outer glows by default.
* NO pure black (`#000000`).
* NO oversaturated accents.
* NO custom mouse cursors.

### 9.B Typography
* AVOID Inter as default.
* Serif constraints: editorial / luxury / publication only.

### 9.C Layout & Spacing
* NO 3-column equal feature cards.

### 9.D Content & Data
* NO generic names ("John Doe", "Acme", "Nexus").
* NO filler verbs ("Elevate", "Seamless", "Unleash").

### 9.E External Resources
* NO hand-rolled SVG icons.
* NO div-based fake screenshots.

### 9.F Production-Test Tells (banned outright)
* NO version labels in hero (V0.6, BETA).
* NO section-number eyebrows (00 / INDEX, 001 · Capabilities).
* NO middle-dot (·) as default separator.
* NO decorative colored status dots.
* NO `<br>`-broken-and-italicized headlines as default.
* NO vertical rotated text.
* NO crosshair / hairline grid lines as decoration.
* NO "Quietly in use at" / "Quietly trusted by" social-proof headers.
* NO weather / locale strips.
* NO version footers on marketing pages.
* NO decoration text strip at hero bottom.
* NO scoring/progress bars with filled background tracks.
* NO scroll cues.
* NO pills/labels overlaid on images.
* NO section-numbering eyebrows.

### 9.G EM-DASH BAN
**Em-dash (—) is COMPLETELY banned.** Zero em-dashes anywhere visible to the user.

## 10. REFERENCE VOCABULARY (Pattern Names)

Hero Paradigms: Asymmetric Split, Editorial Manifesto, Kinetic-Type, Curtain-Reveal, Scroll-Pinned.
Navigation: Mac OS Dock Magnification, Magnetic Button, Dynamic Island.
Layout: Bento Grid, Masonry, Split-Screen Scroll, Sticky-Stack.
Scroll Animations: Sticky Scroll Stack, Horizontal Scroll Hijack, Zoom Parallax.

## 11. REDESIGN PROTOCOL

### 11.A Detect the Mode
* **Greenfield** - no existing site. Dial baseline from Section 1.
* **Redesign - Preserve** - modernise without breaking brand. Audit first.
* **Redesign - Overhaul** - new visual language, preserve content and IA.

### 11.B Audit Before Touching
Document: Brand tokens, Information architecture, Content blocks, Patterns to preserve/retire, SEO baseline.

### 11.C Preservation Rules
* Do not change IA unless asked.
* Extract brand colors before applying Section 4.2.
* Preserve copy voice unless asked for rewrite.
* Honor existing accessibility wins.
* Respect existing analytics events.

### 11.D Modernisation Levers (priority order)
1. Typography refresh
2. Spacing & rhythm
3. Color recalibration
4. Motion layer
5. Hero & key-section recomposition
6. Full block replacement

## 12. THE BLOCK LIBRARY

Reference vocabulary names patterns. Block Library implements them. Schema: `skills/taste-skill/blocks/<category>/<pattern>.md`.

Required frontmatter: name, category, dial_compatibility, when_to_use, not_for, stack.
Required body: Visual sketch, Props API, Code sketch, Mobile fallback, Motion variants, Dark-mode notes, Anti-patterns, References.

## 13. OUT OF SCOPE

This skill is NOT for: Dashboards / dense product UI, Data tables, Multi-step forms, Code editors, Native mobile, Realtime collab UIs.

## 14. FINAL PRE-FLIGHT CHECK

Run this matrix before outputting code. **NOT OPTIONAL.**

- [ ] Brief inference declared?
- [ ] Dial values explicit?
- [ ] Design system chosen?
- [ ] ZERO em-dashes anywhere?
- [ ] Page Theme Lock: ONE theme?
- [ ] Color Consistency Lock: one accent?
- [ ] Shape Consistency Lock: one radius system?
- [ ] Button Contrast Check: WCAG AA?
- [ ] CTA Button Wrap: no wraps at desktop?
- [ ] No Duplicate CTA Intent?
- [ ] Eyebrow count ≤ ceil(sectionCount / 3)?
- [ ] Split-Header Ban obeyed?
- [ ] Zigzag Alternation Cap obeyed?
- [ ] Logo wall = logo only?
- [ ] Bento Background Diversity?
- [ ] Copy Self-Audit passed?
- [ ] Motion motivated?
- [ ] Marquee max-one-per-page?
- [ ] Navigation on ONE line, ≤ 80px?
- [ ] Section-Layout-Repetition check?
- [ ] Real images used?
- [ ] No AI Tells from Section 9?
- [ ] Reduced motion wrapped for MOTION > 3?
- [ ] Dark mode tested?
- [ ] Mobile collapse explicit?
- [ ] Viewport stability: min-h-[100dvh]?
- [ ] Core Web Vitals plausibly hit?
- [ ] One design system per project?
