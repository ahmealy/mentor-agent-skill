# claude-mentor

> A Claude Code skill that makes the AI teach you — instead of doing it for you.

---

## The Problem

AI coding tools are quietly degrading developer skills through **cognitive offloading** — the brain stops doing work it delegates to an external tool.

A 2026 study found programmers who used AI to learn a new skill scored **17% lower** on tests than those who didn't, across all experience levels. The MIT Media Lab found ChatGPT users had the lowest brain engagement of any group tested. The METR study found experienced developers took **19% longer** on tasks when using AI.

The issue isn't AI. It's using it as an answer machine instead of a thinking partner.

---

## The Fix

`/mentor` switches Claude Code into Socratic mentor mode. It never writes code. It never gives you the answer. It asks questions, escalates hints progressively, and forces you to build a real mental model — not just a working solution you don't understand.

---

## Install

```bash
mkdir -p ~/.claude/skills/mentor
cp SKILL.md ~/.claude/skills/mentor/SKILL.md
```

Restart Claude Code. You're done.

---

## Usage

```
/mentor <topic>     Start a session
/mentor exit        End session and log weak areas
```

**Example:**
```
/mentor why my useEffect is running on every render
```

Claude will not tell you the answer. It will ask what you think `useEffect` does, where you'd expect the dependency array to matter, and what you notice about how your component re-renders. By the time you find the bug, you'll own the knowledge.

---

## How It Works

### Hint escalation

Claude escalates through four tiers — only moving forward when you're genuinely stuck:

| Tier | What it does |
|------|-------------|
| 1 — Conceptual | Asks what you think/expect |
| 2 — Directional | Points you toward where to look |
| 3 — Structural | Points to a specific file or function |
| 4 — Near-answer | Explains the mechanism in plain language |
| Fallback | Full conceptual explanation, still no code |

### Guess detection

If you guess — *"maybe it's async?"* — Claude doesn't confirm. It asks: *"What made you think that?"* You need a reason, not a lottery ticket.

### Weak area log

When you exit, Claude appends to `~/.claude/mentor_log.md`:

```markdown
## 2026-03-15 — useEffect dependency array
Weak areas:
- React re-render cycle (reached Tier 3)

Solid:
- Dependency array syntax (self-solved)
```

Over time, this file becomes a map of where your understanding is thin.

---

## What Claude will never do in mentor mode

- Write code
- Produce pseudocode or code blocks
- Give a complete solution, even as an "example"
- Cave to "just tell me" — it offers the next hint tier instead

---

## Companion Skills

| Skill | What it does |
|-------|-------------|
| `/critique` | Audits AI-generated code before you ship it |
| `/rubber-duck` | You explain the problem first — Claude listens before it helps |

Both follow the same philosophy: keep you in the driver's seat.

Install them the same way — copy their `SKILL.md` into `~/.claude/skills/<name>/`.

---

## The Philosophy

> *"Just as athletes still perform basic drills, the only way to maintain an instinct for coding is to regularly practice the grunt work."*
> — Luciano Nooijen, engineer at Companion Group

`/mentor` is a drill. The point isn't the tool — it's the habit of staying cognitively engaged while you use AI.

---

## Contributing

PRs welcome. Especially interested in:
- Improvements to the hint escalation language
- Additional companion skills (`/architect`, `/challenge`, `/postmortem`)
- Translations of the SKILL.md

---

## License

MIT
