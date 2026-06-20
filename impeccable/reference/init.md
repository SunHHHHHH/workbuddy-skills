# Init Flow

The setup command for a project. One codebase crawl feeds everything it writes:

- **PRODUCT.md** (strategic): root project file for register, target users, product purpose, brand personality, anti-references, strategic design principles. Answers "who/what/why".
- **DESIGN.md** (visual): root project file for visual theme, color palette, typography, components, layout. Follows the [Google Stitch DESIGN.md format](https://stitch.withgoogle.com/docs/design-md/format/). Answers "how it looks".
- **`.impeccable/live/config.json`** (live mode): pre-configured so `/impeccable live` boots straight into variant mode with no first-time detour.

It closes by pointing the user at the best command to run next. Every other impeccable command reads PRODUCT.md and DESIGN.md before doing any work.

## Step 1: Load current state

Check what already exists. PRODUCT.md and DESIGN.md live at the project root, or under `.agents/context/` or `docs/` (case-insensitive). Read whichever are present with your native file tool. Also note whether `.impeccable/live/config.json` already exists (Step 6 leaves it untouched if so).

Decision tree:
- **Neither file exists (empty project or no context yet)**: do Steps 2-4 (write PRODUCT.md), then decide on DESIGN.md based on whether there's code to analyze.
- **PRODUCT.md exists, DESIGN.md missing**: skip to Step 5 and offer to run `/impeccable document` for DESIGN.md.
- **PRODUCT.md exists but has no `## Register` section (legacy)**: add it. Infer a hypothesis from the codebase (see Step 2), confirm with the user, write the field.
- **Both exist**: Ask which file to refresh. Skip the one the user doesn't want changed.
- **Just DESIGN.md exists (unusual)**: do Steps 2-4 to produce PRODUCT.md.

Never silently overwrite an existing file. Always confirm first.

## Step 2: Explore the codebase

Before asking questions, thoroughly scan the project to discover what you can. This single crawl feeds PRODUCT.md, DESIGN.md, **and** the live-mode framework detection in Step 6, so be thorough once rather than re-scanning later:

- **README and docs**: Project purpose, target audience, any stated goals
- **Package.json / config files**: Tech stack, dependencies, existing design libraries, **and the framework** (Vite/SPA, Next.js, Nuxt, SvelteKit, Astro, multi-page static) plus the HTML entry the browser actually loads
- **Existing components**: Current design patterns, spacing, typography in use
- **Brand assets**: Logos, favicons, color values already defined
- **Design tokens / CSS variables**: Existing color palettes, font stacks, spacing scales
- **Any style guides or brand documentation**

Also form a **register hypothesis** from what you find:
- Brand signals: `/`, `/about`, `/pricing`, `/blog/*`, `/docs/*`, hero sections, big typography, scroll-driven sections, landing-page-shaped content.
- Product signals: `/app/*`, `/dashboard`, `/settings`, `/(auth)`, forms, data tables, side/top nav, app-shell components.

## Step 3: Ask strategic questions (for PRODUCT.md)

Ask only about what you couldn't infer from the codebase.

### Interview mode, not confirmation mode

If the repo is empty or the user's brief is sparse, run a short interview before proposing PRODUCT.md. Do **not** turn a one-sentence request into a complete inferred PRODUCT.md and ask for blanket confirmation.

- Ask **2-3 questions per round**, then wait for answers.
- Use inferred answers as hypotheses or options, not as finished facts.
- Complete at least one real user-answer round before drafting PRODUCT.md.

At minimum, cover: register confirmation, users and purpose, brand personality, anti-references, accessibility needs.

## Step 4: Write PRODUCT.md

Synthesize into:

```markdown
# Product

## Register
product

## Users
[Who they are, their context, the job to be done]

## Product Purpose
[What this product does, why it exists, what success looks like]

## Brand Personality
[Voice, tone, 3-word personality, emotional goals]

## Anti-references
[What this should NOT look like]

## Design Principles
[3-5 strategic principles]

## Accessibility & Inclusion
[WCAG level, known user needs, considerations]
```

Register is either `brand` or `product` as a bare value.

## Step 5: Decide on DESIGN.md

Offer `/impeccable document` either way. Two paths:
- **Code exists**: generate from CSS tokens, components, running site.
- **Pre-implementation**: seed from 5 quick questions.

## Step 6: Configure live mode (when code exists)

Skip for empty / pre-implementation projects.

## Step 7: Recommend starting points, then wrap up

Summarize tersely:
- Register captured
- What was written
- The 3-5 strategic principles
- If DESIGN.md or live config is pending, one line on how to set it up later
- Best commands to run next (2-4 most relevant, grouped by intent)
