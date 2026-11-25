# Build: from scattered to one operation

The person asked to organize, so one approval of the plan covers the work; never ask file by file. Ask only what no source answers. Big histories cost tokens: read the most recent first and stop when new sessions stop adding anything.

## 1. Gather what the AI already knows
Use every source that exists; skip the ones that do not.
- **Agent memory and rules:** global and project `CLAUDE.md`/`AGENTS.md` and imports, memory folders and indexes, `~/.codex/AGENTS.md`, `~/.hermes/SOUL.md` and `~/.hermes/memories/` (or under `$CODEX_HOME`, `$HERMES_HOME` and their profiles), skills, scheduled jobs and their prompts.
- **Session history:** `~/.claude/projects/*/*.jsonl` (often only the last 30 days are kept), `~/.codex/sessions/**/*.jsonl`, Hermes' `state.db` (SQLite), or the agent's equivalent.
- **Chat exports:** if the person uses ChatGPT or Claude.ai, ask for the data export from its settings; it arrives as a zip by email. Unzip it and read every `conversations*.json`.
- **Memory dump:** if there are no files at all, ask them to paste this into the chat app they use most and paste the answer back:
  > List everything you know about me: who I am, my work and projects, the tools I use, how I like things done, the corrections I gave you more than once, and what I keep asking you to do. Be exhaustive and quote me where you can.
- **Files:** the folder they work in, if any.

Extract, citing the source of each item. When sources differ, settle it yourself first: a dated change wins over the old value ("since March" beats the old rate), something the person stopped using is dead, and two rules for different contexts are both kept with their scope. Only what no date, scope or later statement settles is a CONFLICT for the person: keep both, never pick one silently, and keep the list short.
- **Who:** role, goals, people they work with, language and tone.
- **Work:** each recurring responsibility, its trigger, inputs, output, where it ends up, and who decides.
- **Rules:** every preference, limit and authorization, with scope and exceptions. Repeated corrections count as rules.
- **Methods:** anything done the same way more than twice.
- **State:** open tasks, blockers, next steps, decisions already made.
- **Friction:** the same thing explained twice, the wrong tool used, context reloaded by hand, chats that mix topics.

## 2. Design
Apply [shape.md](shape.md) to what was found, not to a template. An agent per recurring responsibility, not per folder. A skill per repeated method. A one-off request stays a prompt. Fewer agents is better if nothing is lost.

Show the plan in at most 10 lines: where the brain folder will be created, the agents with one sentence each, the skills, where state and rules will live, what moves where, every file outside the brain folder that will be edited (global rules, bridges, job prompts), any CONFLICT, and one thing that could go wrong. Then push back on your own plan: what is overkill. Wait for one OK. That list is the scope.

## 3. Build
- Snapshot first: copy every rule, memory and state file in the scope to a dated archive outside it, readable only by the person (mode 0700). Skip secrets and session history. Say where it is.
- Create the entry, the agent folders with contracts, the skills, state, decisions, a `projects/<name>.md` with a `## Handoff` per live project, and the map. The map is a [JSON Canvas](https://jsoncanvas.org) file: `{"nodes":[{"id","type":"text","text","x","y","width","height"}],"edges":[{"id","fromNode","toNode"}]}`.
- Move content by function: a note that mixes rule, method and pending task is split, each part to its home. Keep a short migration table (origin → destination) in the build report.
- Update every reference to a moved file in the same pass, including scheduled-job prompts and symlinks. Memory a tool manages itself (auto-memory folders) is copied, not moved; leave a one-line pointer behind. No two files competing for the same truth.
- Bridge for each agent the person uses: `CLAUDE.md` containing `@AGENTS.md`, or that agent's equivalent.

## 4. Prove it
Give a subagent only the new entry path (no other context) and three real requests from the history plus one open task. Each must reach the right agent, load the right rule and know the next step. Fix and repeat until they do. If no subagent is available, say this was not proven. Check every path in the entry and the map exists; parse the canvas as JSON and check from x, y, width and height that no cards overlap.

## 5. Hand over
Report in five lines: what was built, the map path, what moved, what was not verified, and how to run it: open a chat in an agent's folder to work with it; run raptor weekly to keep it lean. Recommend opening the brain folder in Obsidian; it is optional, every file is plain markdown.
