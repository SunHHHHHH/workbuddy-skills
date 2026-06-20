---
name: to-prd
description: Turn the current conversation into a PRD and publish it to the project issue tracker — no interview, just synthesis of what you've already discussed.
disable-model-invocation: true
---

# to-prd

This skill takes the current conversation context and codebase understanding and produces a PRD. Do NOT interview the user — just synthesize what you already know.

## Process

1. Explore the repo to understand the current state of the codebase, if you haven't already. Use the project's domain glossary vocabulary throughout the PRD, and respect any ADRs in the area you're touching.

2. Sketch out the seams at which you're going to test the feature. Existing seams should be preferred to new ones. Use the highest seam possible. The fewer seams across the codebase, the better.

Check with the user that these seams match their expectations.

3. Write the PRD using the template below, then publish it to the project issue tracker. Apply the `ready-for-agent` triage label.

## PRD Template

**Problem Statement** — The problem that the user is facing, from the user's perspective.

**Solution** — The solution to the problem, from the user's perspective.

**User Stories** — A LONG, numbered list of user stories in format: "As an <actor>, I want a <feature>, so that <benefit>"

**Implementation Decisions** — modules to build/modify, interface changes, architectural decisions, schema changes, API contracts. Do NOT include specific file paths or code snippets (exception: prototype snippets that encode key decisions).

**Testing Decisions** — What makes a good test, which modules tested, prior art.

**Out of Scope** — What's explicitly not in this PRD.

**Further Notes** — Any additional notes.
