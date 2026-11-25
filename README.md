# raptor

**Your AI already knows how you work. Raptor turns that into an operation, then keeps it lean.**

Raptor 1 had every pipe on the outside. Raptor 3 makes more thrust with a fraction of the parts. Most AI setups are Raptor 1: one chat for everything, rules scattered across memory and old prompts, the same correction typed for the tenth time, a rules file that only grows.

Raptor is one skill for any agent that loads skills (Claude Code, Codex, Hermes, or your own) with two modes:

| | **build** · once | **trim** · weekly |
|---|---|---|
| For | No structure yet, or a mess | A structure that keeps growing |
| Reads | Memory, chat history, exports, rules, files | What loads at chat start, last week's sessions |
| Does | One entry, agents with contracts, skills, state, decisions, a map | Cleans junk, fixes dead paths, finds rules nobody follows |
| You do | Approve one 10-line plan | Answer `apply 1, 3` |

## Build: everything your AI knows, organized

Raptor reads what already exists: your agent's memory and rules, your session history (Claude Code, Codex, Hermes), your ChatGPT or Claude.ai export. The more you've used AI, the more it finds; it reads newest first and stops when history stops adding anything. No files at all? It hands you one prompt to paste into the chat you use most:

> List everything you know about me: who I am, my work and projects, the tools I use, how I like things done, the corrections I gave you more than once, and what I keep asking you to do.

From that it finds your recurring responsibilities, your methods, your rules (including the ones you only ever said as a correction) and your open work, and builds this:

```
brain/
  AGENTS.md          one entry: who you are, which agent handles what
  Map.canvas         your whole operation on one screen
  State.md           live, blocked, next
  Decisions.md       numbered, dated
  agents/writer/
    AGENTS.md        contract: input, output, checks that mean done, what not to touch
    memory.md        every open item it owns
    cases.md         every correction you gave it, so you never give it twice
    skills/
```

Then it walks three of your real past requests through the new entry, from a fresh chat, and fixes the structure until each lands on the right agent with the right rules.

It's all plain markdown. Open the folder in [Obsidian](https://obsidian.md) and it's a second brain with a live map; skip Obsidian and it still works.

The shape is not theory: it's the author's own setup, one entry and four agents with their own memory and corrections, in daily use since October 2026.

## Trim: rules only grow, until you cut them

Every mistake adds a rule. Nobody removes one. Six months in, each chat opens by reading thousands of words of instructions for tools you dropped and bugs that got fixed, and dead rules compete with the ones that matter.

Every week, trim:

1. **Measures** everything loaded at chat start and names the file that grew.
2. **Fixes on its own:** shrinks handoffs to live work + next step, trashes `*.bak` / `* copy*` / empty folders nothing points to, repairs dead paths.
3. **Checks:** mines last week's sessions for the correction you gave twice, the wrong skill, the method redone by hand; holds rules against their evidence.
4. **Proposes** at most 5 cuts, each with file, current text, new text and evidence.

A real run on the author's setup:

```
Words loaded at start: 8,274 → 6,866  (-17%)
Removed: rules for a retired agent, an old model-rotation scheme,
         a "safe zone" policy nothing used anymore
Not followed: none this week
```

Three rules about things that no longer existed, read at the start of every chat. An agent that reads a dead rule can follow it.

A proposal looks like this:

```
2. AGENTS.md, "Model rotation" (212 words)
   Current: "Rotate between models every 3 tasks to balance quota..."
   New:     (remove)
   Why:     that model was dropped weeks ago; the subagent log
            shows zero rotations in 30 days (logs/subagents.log)
```

You type `apply 2`. Done.

## Install

Markdown only. No code, no dependencies, no extra services: your files stay where they are, and only your agent's own model sees what it reads.

```bash
# Claude Code
git clone https://github.com/defiphill/raptor ~/.claude/skills/raptor
```

```bash
# Codex
git clone https://github.com/defiphill/raptor ~/.codex/skills/raptor
```

```bash
# Hermes
git clone https://github.com/defiphill/raptor ~/.hermes/skills/productivity/raptor
```

Any other agent: clone it where it loads skills, or tell it "read raptor/SKILL.md and run it here".

Then, in the folder you want organized, ask your agent to "run the raptor skill" (`/raptor` in Claude Code). It picks the mode: build if there's no structure yet, trim if there is. Run trim weekly; Friday works. On a schedule with nobody around, it cleans and measures, then leaves the proposals for your next chat.

## Safety

- Build shows you the plan in 10 lines, including every file it will touch outside the new folder, and waits for one OK. It snapshots your rules, memory and state before moving anything.
- Trim never edits a rule or memory file without your `apply`.
- Never opens secrets, never grants a new permission to pay, send, publish or touch production.
- Never `rm`: removals go to the Trash, and every removed path is in the report. In a git repo, changes stay uncommitted for you to review.
- Never drops a rule, decision, open task or unique fact without proof it's dead. When two of your rules disagree, it asks you instead of picking one.

## License

MIT
