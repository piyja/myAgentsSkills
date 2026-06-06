---
name: learn-by-doing
description: Attach learning blocks to every meaningful code or file change made during a task. Use when user wants to learn while Claude works, when user says "explain as you go", "teach me", "learn by doing", or when active for a session. After each non-trivial action, emit a prominently formatted LEARNING block covering the concept, the why, and the takeaway.
---

# Learn By Doing

## What This Skill Does

After every meaningful code or file change, emit a **LEARNING BLOCK** — a crisp, prominent callout that surfaces the transferable concept behind what just happened.

## When to Emit a Learning Block

Emit after:
- Any file edit or creation that uses a non-obvious pattern
- A shell command whose flags/behavior is worth knowing
- A refactor, fix, or structural decision with a reusable principle
- An API, config, or tool usage the user likely hasn't seen before

Skip for: trivial renames, obvious syntax fixes, boilerplate scaffolding.

## Learning Block Format

Always use this exact format — no variation:

```
╔══════════════════════════════════════════════╗
║  📚 LEARNING                                 ║
╠══════════════════════════════════════════════╣
║  WHAT:    <concept name, 1 line>             ║
║  WHY:     <why this approach, 1-2 lines>     ║
║  TAKEAWAY: <rule you can reuse, 1 line>      ║
╚══════════════════════════════════════════════╝
```

- **WHAT** — name the concept (e.g. "Git interactive rebase", "CSS specificity", "Memoization")
- **WHY** — explain why this was the right move in this context
- **TAKEAWAY** — one portable rule the user can apply elsewhere

## Rules

1. Learning block appears **immediately after** the change, before moving to the next step.
2. Keep each field to the line limit — ruthlessly concise.
3. One learning block per distinct concept. If two concepts appear in one change, emit two blocks.
4. Never pad. If there's nothing worth learning, skip the block entirely.
5. Phrase TAKEAWAY as a rule: "Always X when Y", "Use X instead of Y when Z", "X prevents Y".

## Example

After adding a debounce to an input handler:

```
╔══════════════════════════════════════════════╗
║  📚 LEARNING                                 ║
╠══════════════════════════════════════════════╣
║  WHAT:    Debouncing                         ║
║  WHY:     Fires the handler once after the   ║
║           user stops typing, not on every   ║
║           keystroke — prevents excess calls  ║
║  TAKEAWAY: Use debounce for input/scroll     ║
║           events; use throttle for resize   ║
╚══════════════════════════════════════════════╝
```

## Activation

When this skill is active, announce it once at the start:

> **Learn-by-doing mode active.** I'll surface a learning block after each meaningful change.

Then proceed with the task normally — learning blocks slot in after each relevant action.
