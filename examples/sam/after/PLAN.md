# Raptor plan (build mode) for Sam

1. Brain folder: `brain/` (inside this folder). Entry `brain/AGENTS.md` + `CLAUDE.md` bridge, `Map.canvas`, `State.md`, `Decisions.md`.
2. Agents: `newsletter` (Small Screens), `client-work` (briefs, proposals/invoices, case studies), `critique` (Figma feedback).
3. Skill: `brief-structure` (one copy, used by briefs and case studies). Projects: `fernway` (live), `brightloop` (closed).
4. Rules live once in the entry (global) or in the owning agent's contract. State: `State.md` + each agent's `memory.md`. Corrections seeded into each `cases.md` from memory-dump counts.
5. Moves: CLAUDE.md rules split by function; notes/todo.md folded into State/memory/handoff; notes stay in `notes/`.
6. Files edited outside `brain/`: `CLAUDE.md` (becomes `@brain/AGENTS.md`). Removed to `.raptor-trash/`: `notes/fernway-brief copy.md` (byte-identical), `notes/old.bak` (0 bytes), `notes/todo.md` (fully migrated), empty `notes/archive-2025/`.
7. Snapshot first: `_snapshot-2026-11-25/` (mode 0700) with CLAUDE.md, memory-dump.md and notes/.
8. Settled by date/scope: rate 3,200/week since March (2,800 is old; 3,600 planned from January); Linear stopped in August (rule dropped); Brightloop done (rules kept in its closed project note); spelling: British in newsletter, American for US clients; notes in markdown, client docs in Notion.
9. CONFLICT for you: newsletter word limit, 900 (your memory dump) vs 1,000 (CLAUDE.md). Both kept in Decisions; 900 applied until you say.
10. Could go wrong: the `prompts/mj.md` moodboard template and `tokens-v2.json` do not exist in this folder; I only note the paths, I cannot confirm them.
Overkill check: no separate agents for case studies or invoices (same client-work contract); no per-issue project notes.
