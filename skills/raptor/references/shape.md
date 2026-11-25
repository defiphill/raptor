# Shape of a lean operation

A shape, not a tree. Keep names and folders that already work; add only what something real needs.

```
brain/
  AGENTS.md        entry: who the person is (5 lines), routes, where truth lives, global rules
  CLAUDE.md        @AGENTS.md (one bridge per agent tool in use)
  Map.canvas       the operation at a glance (Obsidian canvas, optional)
  State.md         one screen: live, blocked, next
  Decisions.md     numbered, dated, one line each
  agents/<name>/
    AGENTS.md      the contract
    memory.md      state of every open item this agent owns
    cases.md       every correction: rule, evidence, where it applies
    skills/<skill>/SKILL.md
  projects/<name>.md   with a ## Handoff of at most 30 lines
```

## The entry
Short. Who (by name; never guess pronouns, use "they" unless the person stated theirs), then routes: "a request about X → `agents/x/`". Global rules live here once and nowhere else. It never makes every chat read every agent.

## An agent
One recurring responsibility, its own context, its own deliverable. Its contract says: what it does, input, output, the checks that mean done (written before it runs), and what it must not touch. Its memory lives in files, never in a chat: when a chat gets long, open a new one in the agent's folder. It starts by preparing work for the person's approval and earns autonomy once its output passes without corrections.

## A skill
A method, transferable between tasks: trigger, inputs, steps, acceptance. No task data inside. One copy, shared by every agent that uses it.

## Corrections
Each time the person repeats a rule, says "continue", or fixes what the agent should have known, it goes into that agent's `cases.md`, and the rule that let it happen is fixed in place, never patched with a dated paragraph on top. The count per agent shows which one to fix first.

## Habits the shape assumes
- One topic per chat. Day to day, the person talks to the agent directly.
- The raw source wins over any summary: keep transcripts, exports and the person's exact words; derive from them.
- Review that can reject: check a result against the contract, return only the failed part, at most three times, then show the person the diagnosis.

## The map
One card per agent and per shared skill or tool, one sentence each: what it does, not today's progress. The person at the top. No card on top of another; check it from the coordinates. Every change to how things run updates the map in the same pass.
