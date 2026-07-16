# Writing a CLAUDE.md That the Agent Actually Follows

A `CLAUDE.md` (or `AGENTS.md`) is the instruction file an AI coding agent loads at the
start of **every** session. It's the cheapest lever you have on output quality — and the
easiest one to waste.

**Grab the template:** [`CLAUDE.md.example`](./CLAUDE.md.example) — copy it into your repo
root as `CLAUDE.md` and replace every `‹fill in›`.

---

## The one test: project file, not persona file

The most common mistake is spending the whole file tuning **how the agent talks** ("be
concise", "no compliments", "be helpful") and none of it on **facts the agent can't guess**.

Verified project facts beat behavioural tuning every time, because:

- Commands and paths are things the agent **will get wrong** if you don't tell it.
- Tone is something modern models mostly get **right on their own**.

If a line would be true of any repo on earth, it's probably not earning its place.

```
                 LOW VALUE  ─────────────────────────►  HIGH VALUE
   "be helpful, be concise"      "run `make check` before      "reuse src/models before
    (model already does this)     you say it's done"            inventing a new type"
```

## Six rules that make instructions stick

1. **Checkable procedure beats uncheckable virtue.**
   "Prove it's correct" → the model *performs* diligence (writes a plausible sentence).
   Instead: *"name the existing service you checked and why it didn't fit."*

2. **Turn vague prohibitions into visibility.**
   "Don't change the schema unless required" is ignorable — everything feels required
   mid-task. Instead: *"if a change touches schema/routes/config, call it out at the top
   of your summary."* Nothing escapes a mandatory callout.

3. **Gate the ceremony.**
   "Always list Risks + Assumptions" bloats a one-line fix. Scope it to
   *schema / API / auth / multi-file* changes. Trivial changes: just do them.

4. **Group into short headed sections.**
   A flat 15-item list means everything is priority, so nothing is. Use
   `Commands / Structure / Code changes / Safety / Communication` — 3–5 bullets each.

5. **Concrete rules survive long context; vague ones decay.**
   Forty tool-calls deep, "be practical" has zero pull. "Run the type checker before
   declaring done" still fires — it's a concrete action at a concrete moment.

6. **Add a definition of done and a scope-stop rule.**
   Without "done = tests pass + …", the agent decides when to stop. Without "fix only what
   the task requires", it "improves" three adjacent things you didn't ask about — a costlier
   failure than verbosity.

## Keep it lean

`CLAUDE.md` loads every session, so every line is a recurring token cost and, past a point,
adherence drops. Treat it as **one page of concrete facts**, not a wiki.

- When a rule file grows, push detail **down** into a linked doc or **up** into a reusable
  skill — not into the always-on page.
- Keep shared, cross-tool knowledge in `AGENTS.md` and import it with a literal `@AGENTS.md`
  line, so Claude Code, Cursor, Copilot, and Codex all read one source.
- Grow rules from **observed** failures: add a line the second time you make the same
  correction; delete lines that never fire. A `CLAUDE.md` is a garden, not a constitution.

## Never put in it

Secrets, tokens, or production hostnames. The file ships to the model provider every session
and to your teammates through git.

---

*The `.example` file is stack-neutral (generic `src/…` placeholders). Swap them for your
real commands and paths — a wrong command in `CLAUDE.md` is worse than none.*
