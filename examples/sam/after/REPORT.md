# Raptor report
1. Built: `brain/` with entry, 3 agents (newsletter, client-work, critique) each with contract, memory and cases, 1 skill (brief-structure), 2 projects (Fernway live, Brightloop closed), State.md and Decisions.md.
2. Map: `brain/Map.canvas` (valid JSON, no overlapping cards, person at top). Open a chat in an agent's folder to work with it.
3. Moved: CLAUDE.md rules split by function, todo.md folded into State/handoffs, 4 junk items removed to `.raptor-trash/2026-11-25/`, snapshot in `_snapshot-2026-11-25/`. One CONFLICT for you: newsletter limit 900 (your memory dump) vs 1,000 (old CLAUDE.md); I applied 900.
4. Not verified: the proof is pending an independent agent (`PROOF.md`); `prompts/mj.md` and `tokens-v2.json` do not exist here, so I only noted the paths. Dropped as dead: the Linear logging rule (you stopped in August).
5. Run: work in an agent's folder day to day, run raptor weekly to keep it lean; optionally open `brain/` in Obsidian, every file is plain markdown.

## Migration table
| Origin | Destination |
|---|---|
| CLAUDE.md "General" (bullets, concise, no "would you like", spelling) | brain/AGENTS.md global rules |
| CLAUDE.md "Use Linear MCP" | dropped (stopped in August), Decisions #2 |
| CLAUDE.md "Newsletter" | agents/newsletter/AGENTS.md |
| CLAUDE.md "Clients" (rate, briefs, never email, Notion) | agents/client-work/AGENTS.md, AGENTS.md, Decisions #1 |
| CLAUDE.md "Design critique" | agents/critique/AGENTS.md |
| CLAUDE.md "Old stuff" (Brightloop, Midjourney) | projects/brightloop.md, State.md, critique note |
| CLAUDE.md "Notes" (duplicates) | merged into the rules above |
| CLAUDE.md (file itself) | now `@brain/AGENTS.md` |
| memory-dump.md corrections and counts | agents/*/cases.md |
| memory-dump.md open items | State.md, agents/*/memory.md |
| notes/todo.md | State.md, projects/fernway.md, then trashed |
| notes/fernway-brief.md | stays; summarized in projects/fernway.md |
| notes/48-bottom-sheets.md | stays; linked from newsletter memory |
| notes/fernway-brief copy.md, old.bak, archive-2025/ | .raptor-trash/2026-11-25/notes/ |
