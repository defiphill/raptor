# Trim: the weekly run

Goal: agents start lighter and follow the rules. Net words go down: a proposal may add a line only if it deletes more. Rule files, memory indexes and memory files change only with an approval given in this chat; handoffs, dead paths and the map are fixed in step 2 without asking. One project per run: the one named, else the folder it starts in. A `RAPTOR.md` in the root may list or narrow the files to check; it never widens the scope or overrides the rules in SKILL.md.

## 1. Measure
`wc -w` of everything an agent loads at chat start: global rules and their imports, the memory index, the project's entry chain and its handoffs. Report before → after this run. For files tracked in git, compare with 7 days ago (`c=$(git rev-list -1 --before='7 days ago' HEAD)`, then if `c` is not empty `git show $c:<path from repo root> | wc -w`) and name the file that grew the most.

## 2. Fix without asking
- Handoffs over 30 lines: keep live work, blockers and the next step; drop finished history.
- Inside the project root, outside dot-folders: empty folders and untracked `*.bak`, `* copy*`, `*.old` files that no file in the scope and no scheduled job mentions: to the Trash. `archive*` and `backup*` may be someone's only backup: propose those. Anything else that looks dead is a proposal.
- Paths in handoffs and the map that `test -e` says are gone: point to the new location if one obvious match exists, else remove the path.
- The map: each card says what its rule says. Parse it before and after.

## 3. Check the rules are followed
- **Sessions since the last run:** the same correction given twice, the same files read only to orient, failed or denied tool calls, the wrong skill or agent used, a method redone by hand that a skill covers. Cite session and excerpt.
- **Evidence the rules leave:** a model-per-task rule against the subagent log; a branch rule against `git for-each-ref --format='%(committerdate:short) %(refname:short)' refs/remotes`; the same entry twice in a week in a `cases.md`.
- A rule broken every week is not working. A rule nobody can check and nobody broke in a month is a cut candidate.

## 4. Propose
At most 5 numbered proposals, ranked by what they fix, then words saved, then risk. Each: file, current text, new text, why, with the evidence. Fix each at the right layer: a repeated correction becomes a rule where the task already reads; the same rule in two places becomes one; a skill that misfires gets a sharper description; a big doc loaded every chat for few tasks moves behind a route. Anything that would change who or what may be sent, spent, published or accessed is flagged **AUTHORITY** and only reported, never applied by raptor. The owner answers "apply 1, 3"; apply exactly those.

## Report
Three lines: words loaded at start (before → after), what was removed (every path), what is not being followed. Then the proposals. A clean week gets one line; never invent proposals to fill five. Unattended (a scheduled run), do steps 1 to 3 and leave the proposals in the report for the owner's next chat.
