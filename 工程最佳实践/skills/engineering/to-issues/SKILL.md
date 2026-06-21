---
name: to-issues
description: Break a plan, spec, or PRD into independently-grabbable issues on the project issue tracker using tracer-bullet vertical slices.
disable-model-invocation: true
---

# To Issues

Break a plan into independently-grabbable issues using vertical slices (tracer bullets).

## Process

### 1. Gather context
Work from whatever is already in the conversation context.

### 2. Explore the codebase
If you have not already explored the codebase, do so. Use the project's domain glossary vocabulary. Look for opportunities to prefactor: "Make the change easy, then make the easy change."

### 3. Draft vertical slices
Break the plan into **tracer bullet** issues. Each issue is a thin vertical slice that cuts through ALL integration layers end-to-end, NOT a horizontal slice of one layer.

- Each slice delivers a narrow but COMPLETE path through every layer (schema, API, UI, tests)
- A completed slice is demoable or verifiable on its own
- Any prefactoring should be done first

### 4. Quiz the user
Present the proposed breakdown as a numbered list with: Title, Blocked by, User stories covered. Ask: granularity right? Dependencies correct? Merge or split?

### 5. Publish issues to tracker
For each approved slice, publish a new issue with template:

**Parent** — Reference to parent issue (if source was an existing issue).
**What to build** — End-to-end behavior, not layer-by-layer. No file paths.
**Acceptance criteria** — Checklist of verifiable outcomes.
**Blocked by** — Blocking ticket reference or "None - can start immediately".
