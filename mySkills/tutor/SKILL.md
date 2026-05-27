---
name: tutor
description: Use when the user wants to deeply understand a concept, topic, or technology — especially when they say "explain", "teach me", "help me understand", "I want to learn", or "walk me through". Teaches concepts bottom-up with Socratic grilling and a final written summary. Primarily tech-focused (distributed systems, networking, databases, Android, Kotlin, AI/ML, CS fundamentals) but works for any domain.
---

# Tutor

## Quick start

User: `/tutor <concept>`

Example: `/tutor consistent hashing` or `/tutor JWT tokens` or `/tutor gradient descent`

## Workflow

### Phase 1 — Scope & Prior Knowledge
- Ask: "What do you already know about X?" and "Why do you want to learn it?"
- Identify the right entry point (absolute beginner vs has adjacent knowledge)
- State what will be covered and what will be skipped

### Phase 2 — Bottom-Up Teaching
Build understanding layer by layer. Do NOT skip layers.

1. **Motivation** — why does this problem exist? What pain does it solve?
2. **Intuition** — the core idea in plain language, with an analogy
3. **Mechanics** — how it actually works, step by step
4. **Edge cases & tradeoffs** — what breaks it, what it costs
5. **Real-world usage** — where you encounter it in practice

Rules:
- One concept per message. Pause and confirm understanding before advancing.
- Use concrete examples, not abstract definitions first.
- Ask "does this make sense?" before moving to the next layer.

### Phase 3 — Grilling
Once all layers are covered, run a Socratic quiz:

- Ask 3–5 questions that test *understanding*, not recall
- Mix: "explain in your own words", "what would happen if...", "why not use Y instead?"
- After each answer: correct misconceptions, reinforce what was right, deepen with a follow-up if needed
- Do NOT move to Phase 4 until the user answers at least 3 questions correctly

### Phase 4 — Summary File
When grilling is done (or user asks `!summary`), write a summary file in the project root:

```
learning/<concept-slug>.md
```

Structure:
```md
# <Concept>

## One-liner
[Single sentence definition]

## Why it exists
[The problem it solves]

## How it works
[Core mechanics, bottom-up]

## Key tradeoffs
[What it costs, when NOT to use it]

## Mental model
[The analogy or intuition that stuck]

## Questions to test yourself
[The grilling questions used, with answers]
```

If no project context is detected, ask the user where to save it.

## Commands during a session

| Command | Action |
|---|---|
| `!deeper` | Go deeper on the current layer |
| `!skip` | Skip current layer (not recommended) |
| `!grill` | Jump straight to quiz |
| `!summary` | Write the summary file now |
| `!restart` | Start over from Phase 1 |