---
name: raptor
description: Weekly trim for an agent rule system, like Raptor 1 to 3 - fewer parts, same thrust. Measures what agents load at the start of every chat, cuts bloated handoffs and copy files, fixes dead paths, checks the rules are actually followed, and proposes at most 5 rule cuts; it never edits a rule unless the owner approves that proposal in the same chat. Use for /raptor, "run raptor", "trim the rules", "clean up the agent setup", or a weekly run.
---

# /raptor

Goal: agents start lighter and follow the rules. Remove parts; never add any (no new rules, files, scripts, notes or jobs). Reply short, in the owner's language. Each run covers ONE project: the one the prompt names, else the folder it starts in.

## Scope
Find these by reading, not guessing. If the project root has a `RAPTOR.md`, it lists them and wins.
- **Rules:** the agent's global rules file (e.g. `~/.claude/CLAUDE.md`, `~/.codex/AGENTS.md`, `~/.hermes/SOUL.md`) and everything it imports, the project's `AGENTS.md`/`CLAUDE.md` chain (root and nested), and any file those name as "read first".
- **Memory:** whatever memory the agent loads at start (e.g. a `MEMORY.md` index, a memories folder).
- **Handoffs:** `HANDOFF.md`, state or status notes, `## Handoff` sections the rules point to.
- **Map:** any diagram or canvas the rules say must stay current. Optional.
- **Corrections:** `cases.md`, `lessons.md` or similar, if the rules keep one. Optional.
- **Owned areas:** folders the rules say belong to someone else or another agent. Read-only here.

## Never
Edit a rule or memory file without an approval given in this chat. Touch secrets (`.env*`, credentials, key-bearing files), hooks, code, backups, or anything outside the project. Commit, push, delete or rewrite branches: inside a git repo, leave every change as an uncommitted diff for the owner to review.

## 1. Measure
`wc -w` of everything an agent loads at chat start: global rules, their `@` imports, the memory index, the project's rules chain and its handoffs. Report words, before → after this run. If a file is tracked in git, compare it with its version from 7 days ago (`git show $(git rev-list -1 --before='7 days ago' HEAD):<file> | wc -w`) and name the file that grew the most.

## 2. Fix without asking
- Handoffs outside owned areas, over 30 lines: keep live work, blockers and the next step; drop finished history, with no archive.
- Inside the project only: empty folders, and files or folders named `*.bak`, `* copy*`, `*.old`, `archive*`, `backup*` that no rule, handoff or map mentions, and that git does not track: move to the system Trash (`trash`, `gio trash`, or Finder), never `rm`. Anything else that looks dead is a proposal.
- Paths in handoffs and the map that `test -e` says no longer exist: point to the new location if one obvious match exists, otherwise remove the path.
- The map: each card says what its rule says. Parse it as JSON (or its format) before and after.

## 3. Check the rules are followed
Rules that leave evidence get checked against it, for the last 7 days. Examples:
- A model-per-task rule and a subagent log: models used vs. the rule; reviews run on the same model as the build; builds with no review.
- A branch rule and a repo: `git fetch --prune`, then `git for-each-ref --format='%(committerdate:short) %(refname:short)' refs/remotes`; stale branches the rule forbids.
- A corrections file: the same correction twice in the week means its rule is not working.
A rule nobody can check and nobody broke in a month is a cut candidate.

## 4. Propose
Rule and memory changes, deletions beyond step 2, owned areas: at most 5 numbered proposals, ranked by words saved, then risk; plus up to 3 for owners of owned areas. Each: file, current text, new text, why, with the evidence path. Shortening that keeps every requirement is one bundled item. Mark **AUTHORITY** any change to who or what may be sent, spent, published or accessed. The owner answers "apply 1, 3" in this chat; apply exactly those and nothing else.

## Report
Three lines: words loaded at start (before → after), what was removed, what is not being followed. Then the proposals. If nothing is worth cutting, say so in one line; never invent proposals to fill the five.
