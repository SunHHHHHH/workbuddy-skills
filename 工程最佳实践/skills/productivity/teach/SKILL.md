---
name: teach
description: Teach the user a new skill or concept, within this workspace.
disable-model-invocation: true
argument-hint: "What would you like to learn about?"
---

# Teach

The user has asked you to teach them something. This is a stateful request - they intend to learn the topic over multiple sessions.

## Teaching Workspace

Treat the current directory as a teaching workspace. The state of their learning is captured in:
- `MISSION.md`: The _reason_ the user is interested. Grounds all teaching.
- `./reference/*.html`: Cheat sheets, reference algorithms, syntax, glossaries — compressed learnings designed for quick reference.
- `RESOURCES.md`: High-quality, high-trust resources for knowledge acquisition.
- `./learning-records/*.md`: Non-obvious lessons and key insights, ADR-style (`0001-name.md`).
- `./lessons/*.html`: The primary output — self-contained HTML lessons, one per concept.
- `./assets/*`: Reusable components shared across lessons (stylesheets, quiz widgets, simulators).
- `NOTES.md`: Scratchpad for user preferences and working notes.

## Philosophy

Three pillars: **Knowledge** (from trusted resources), **Skills** (interactive lessons), **Wisdom** (community interaction).

**Fluency vs Storage Strength**: Fluency gives illusory mastery. Build storage strength through:
- Retrieval practice (recall from memory)
- Spacing (distribute practice over time)
- Interleaving (mix related topics — skills only)

## Lessons

Each lesson is a self-contained HTML file: `./lessons/0001-name.html`. Should be **beautiful** (Tufte-style), short, and completable quickly within working memory limits. Each gives a single tangible win tied to the mission.

- Link to other lessons and references via HTML anchors.
- Recommend a primary source (highest-quality resource).
- Include a reminder to ask followup questions.
- Open the file for the user after creation.

## Assets

Reusable components in `./assets/`: stylesheets, quiz widgets, simulators, diagram helpers. **Reuse by default.** A shared stylesheet is the first component every workspace earns.

## The Mission

Every lesson ties to the mission. If `MISSION.md` is empty, question the user about why they want to learn. Missions evolve — update and confirm changes.

## Zone Of Proximal Development

Challenge "just enough." Determine by reading learning records, figuring the right next thing based on the mission.

## Knowledge vs Skills

**Knowledge**: From trusted resources. Difficulty is the enemy. Citations everywhere.
**Skills**: Difficulty is the tool. Effortful retrieval builds storage. Taught through interactive feedback loops — quizzes, guided real-world steps. Feedback must be tight and immediate.

## Acquiring Wisdom

Delegate to **communities** — forums, subreddits, classes, groups. Find high-reputation ones. Respect user preference not to join.

## Reference Documents

The compressed essence of lessons. Glossaries especially essential — once created, adhere to in every lesson.
