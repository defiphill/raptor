# raptor

**Your agent reads every rule you ever wrote, every single chat. Raptor cuts the dead ones.**

A skill for any agent that runs on rule files: Claude Code, Codex, Hermes, or your own. Once a week it trims your setup (`AGENTS.md`, `CLAUDE.md`, memory, handoffs): it measures what loads at chat start, deletes the obvious junk on its own, checks which rules are actually followed, and hands you at most 5 cuts to approve.

```
run raptor
```

## The problem

Every time an agent makes a mistake, you add a rule. Nobody ever removes one.

Six months in, each new chat opens by reading 8,000 words of instructions: rules for tools you dropped, workarounds for bugs that got fixed, handoffs from projects that shipped, three paragraphs that say the same thing. The agent pays for all of it before you type a word, and the more it reads, the less of it it follows.

Then you start fixing that by hand. You spend your evenings tuning the system instead of building with it.

## The fix

Named after SpaceX's Raptor engine: version 3 has fewer parts than version 1 and more thrust. Same idea.

Raptor only removes. It never adds a rule, a file, a script or a job.

| Step | What it does | Asks you? |
|---|---|---|
| **1. Measure** | `wc -w` of everything loaded at chat start: global rules, `@` imports, memory index, project rules, handoffs. Before → after, and which file grew this week. | No |
| **2. Fix** | Shrinks handoffs over 30 lines to live work + next step. Trashes empty folders and `*.bak` / `* copy*` / `*.old` files nothing points to. Repairs or removes dead paths. | No |
| **3. Check** | Holds rules against their evidence: subagent logs, stale branches, the same correction logged twice in a week. A rule that keeps getting broken is not working. | No |
| **4. Propose** | At most 5 numbered cuts, ranked by words saved, then risk. Each shows file, current text, new text and the evidence. | **Yes** |

You answer `apply 1, 3`. It applies exactly those and nothing else.

## Real run

A personal agent setup, one Friday:

```
Words loaded at start: 8,274 → 6,866  (-17%)
Removed: rules for a retired agent, an old model-rotation scheme,
         a "safe zone" policy nothing used anymore
Not followed: none this week
```

The win is not the tokens. It is three rules about things that no longer existed, loaded into every chat, competing for attention with the rules that matter. Dead rules don't just cost space: an agent that reads them can follow them.

A proposal looks like this:

```
2. AGENTS.md, "Model rotation" (212 words)
   Current: "Rotate between models every 3 tasks to balance quota..."
   New:     (remove)
   Why:     that model was dropped weeks ago; the subagent log
            shows zero rotations in 30 days (logs/subagents.log)
```

You read five of these, type `apply 2, 4`, done.

## Install

One markdown file, no code, no dependencies. Clone it into your agent's skills folder:

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

Any other agent: put `SKILL.md` wherever it loads skills from, or just point it at the file: "read SKILL.md and run it here".

Then, inside the project you want trimmed, ask it to run raptor (`/raptor` in Claude Code). Run it weekly; Friday works.

## Safety

- Never edits a rule or memory file without your approval in the same chat.
- Never touches secrets, hooks, code, or anything outside the project.
- Never commits, pushes or deletes branches. In a git repo, everything it does is an uncommitted diff you can review or `git restore`.
- Deletes go to the Trash, never `rm`.
- Never pads the list: a clean week gets a one-line report.
- Any proposal that changes who or what may be sent, spent, published or accessed is flagged **AUTHORITY**.

## Custom setups

Raptor finds your rules by reading your `CLAUDE.md` / `AGENTS.md` chain. If your setup is unusual, drop a `RAPTOR.md` in the project root listing your rules, handoffs, map and logs. It wins over discovery.

## License

MIT
