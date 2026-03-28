---
name: cold-codebase
description: >
  Analyze any abandoned, legacy, or inherited codebase and produce a Revival
  Document — a health report, revival plan, and contribution guide in one.
  Trigger when someone says "analyze this repo," "I inherited this codebase,"
  "is this worth reviving," "help me understand what I've got here," "I found
  an abandoned repo," "this hasn't been touched in years," "I want to pick up
  where someone left off," "can this codebase be saved," or shares a GitHub
  link to a dormant project. Also trigger when someone is taking over a project
  from a previous dev, inheriting technical debt, or asking "where do I even
  start" with an existing codebase.
---

# Cold Codebase

An archaeologist's kit for abandoned, legacy, and inherited projects. Reads a
dormant codebase — code, history, issues, dependencies — and produces one
complete document: what's salvageable, what's broken, which path to take, and
exactly where to start.

---

## Who You're Helping

**Solo dev / vibe coder** — found an interesting abandoned repo. Wants to know:
is this worth it? How much work? Where do I start? Needs plain language, not
jargon.

**Team that inherited a legacy codebase** — from a previous dev, acquisition,
or org drift. Needs a structured assessment they can share and act on
immediately.

Both need the same thing: **clarity without false hope, and a path forward
without overwhelm.**

---

## Phase 1 — Archaeological Dig

Read everything before writing anything. Thoroughness here determines the
quality of everything that follows.

### Read in this order

**1. Surface**
- `README.md` — original vision; is it still accurate to the code?
- `CHANGELOG.md` / `HISTORY.md` — when did active development stop?
- Open issues — what did users actually hit? What never got fixed?
- Closed issues + PRs — patterns of struggle; what was attempted and dropped?
- Any "looking for maintainer" or "archived" notices

**2. Health signals**
- Last commit: date, message, and how long ago
- Commit frequency: steady decline / sudden stop / burst-and-abandon?
- Open vs closed issue ratio — high open count = overwhelmed maintainer
- CI/CD status: passing, failing, or nonexistent?
- Lock files (`package-lock.json`, `Pipfile.lock`, `Cargo.lock`) — how stale?
- Branch structure — active dev branch, or just a forgotten main?

**3. Dependency audit**
- Read `package.json`, `requirements.txt`, `Cargo.toml`, `go.mod` in full
- For each major dep: still maintained? Breaking changes since lockfile?
- Note the ecosystem gap: Node 14 in a Node 20 world is a different problem
  than Node 18 in a Node 20 world
- Flag anything with known CVEs or that is itself archived/abandoned

**4. Code — go deep**
- Entry points: can you trace a clear path from "starts" to "does something"?
- Core business logic: coherent and intentional, or tangled and reactive?
- Data layer: what storage? Schema documented? Migrations in order?
- Tests: exist? Pass? What do they cover — and what don't they?
- Config: hardcoded secrets? Missing `.env.example`? Machine-specific paths?
- Debt signals: `TODO`/`FIXME` comments, commented-out blocks, `temp_`/`old_`
  function names, `backup_` files, dead code that's never called
- Error handling: thoughtful or absent? Silent failures are future landmines
- Security surface: auth patterns, input validation, SQL construction, secret
  management — flag anything that looks like a vulnerability

**5. Architecture**
- Main components and what each one owns
- How they communicate: direct calls, events, queues, HTTP?
- What breaks first if you change X? What is load-bearing?
- What is over-engineered for what the project actually does?
- What will crack under any real load?

**6. Documentation gap**
- Does the setup guide actually work today, or reference extinct tools?
- Are architecture docs accurate to the real code?
- What must someone know to be productive that is nowhere written down?

---

## Phase 2 — Honest Assessment

Form a clear picture before writing. Work through these internally.

**Vitals**
- How long dormant? Ever finished, or abandoned mid-build?
- Still-relevant purpose, or did the world move on?
- Runnable today with reasonable effort?
- Active community (forks, Stack Overflow questions), or truly forgotten?

**The fundamental question — which path?**

| Path | When | What it means |
|---|---|---|
| **Maintain** | Core is solid, debt is manageable | Fix what's broken, update deps, build on top |
| **Fork & modernize** | Good ideas, poor execution | Keep the best parts, rewrite the rest |
| **Rewrite** | Architecture is fundamentally wrong, or maintenance costs more than replacement | Start fresh; use old codebase as a spec |

Commit to one. Don't hedge.

**Classify every significant part**

| Label | Meaning |
|---|---|
| **Keep** | Solid, works — build on top directly |
| **Fix** | Broken but salvageable — estimate the effort |
| **Replace** | Too entangled or wrong approach — rebuild |

**Effort scale**

- **Afternoon** — a few hours, no surprises
- **Weekend** — 1–2 days focused
- **Week** — requires some learning
- **Month** — significant; plan properly
- **Longer** — be specific about why

Always give two numbers: "just get it running" vs "production-ready."

---

## Phase 3 — The Revival Document

One clean Markdown file. Honest, scannable, every section earning its place.

### Structure

```
# Revival Document: [Project Name]

## The Verdict
## Project Snapshot
## Recommended Path
## What Still Works
## What's Broken
## Security Flags
## The Dependency Situation
## Effort Estimate
## Where to Start
## 30-Day Revival Plan
## AI Steering Guide
## Contribution Guide
## Open Questions
```

---

### Section Specs

**## The Verdict**
2–4 sentences. Bottom line for someone who might only read this far. Is it
worth reviving? Core condition? Biggest thing working for it, and against it?
Don't hedge. Don't bury the lede.

> *"Strong core, clear use case, still relevant. Dormant 22 months — serious
> dependency debt, not architectural obsolescence. Auth layer and data model are
> worth keeping. Main obstacles: three abandoned dependencies and a CI setup
> that hasn't passed in over a year."*

---

**## Project Snapshot**
Quick-reference table. No prose.

```
| Field               | Detail                                      |
|---------------------|---------------------------------------------|
| Last commit         | [date] — [N months/years] ago               |
| Language / runtime  | e.g. TypeScript / Node 16                   |
| Dependencies        | [N] total — [N] outdated, [N] abandoned     |
| Tests               | yes/no — [passing % or "unknown"]           |
| Open issues         | [N] open / [N] closed                       |
| CI status           | passing / failing / none                    |
| Original purpose    | [one sentence]                              |
| Dormancy reason     | maintainer left / pivoted / unknown         |
| Recommended path    | Maintain / Fork & modernize / Rewrite       |
```

---

**## Recommended Path**
Which of the three paths, and exactly why. Be direct. If the answer is
uncomfortable, say it with clarity and compassion:
*"This should be rewritten — not because it's bad work, but because the
architecture was built for a problem that has since changed shape."*

If Maintain or Fork: name the one constraint that, if different, would change
the recommendation.

---

**## What Still Works**
Parts that are solid and buildable-on. For each: what it is, where it lives,
why it's still good (specific), what it enables.

Bad: *"The auth module is clean."*
Good: *"JWT auth in `src/auth/` uses standard patterns, handles token refresh
correctly, works without modification once `jsonwebtoken` is updated to v9."*

---

**## What's Broken**
Honest list. For each: what's broken and why, severity
(**blocking** / **significant** / **minor**), effort to fix.
Don't soften this. A broken thing is broken.

---

**## Security Flags**
Separate from general debt — security issues need to be visible.

For each flag: what it is, where it lives, risk level
(**critical** — fix before any deploy / **moderate** — fix before public
exposure / **low** — fix when touching that area), remediation.

Common things to check: hardcoded credentials, string-concatenated SQL, missing
input validation, outdated auth libraries with CVEs, `.env` in git history.

If none found, say so explicitly.

---

**## The Dependency Situation**
Group by status. Focus on what matters, not an exhaustive list.

| Status | Meaning |
|---|---|
| **Fine** | Current, maintained, no action needed |
| **Outdated but safe** | Behind latest, no breaking changes |
| **Needs updating** | Breaking changes — requires code changes |
| **Abandoned** | Dep itself is unmaintained — assess risk |
| **Security risk** | Known CVEs — fix before shipping |

Close with one sentence: *"Dependency situation is [manageable / moderate /
severe]. Estimated time to current: [estimate]."*

---

**## Effort Estimate**
Named work chunks with real estimates.

```
| Work chunk              | What it involves           | Estimate   |
|-------------------------|----------------------------|------------|
| Get it running locally  | Install, fix env errors    | Afternoon  |
| Dependency updates      | Update + fix breakage      | Weekend    |
| Fix auth token bug #34  | Session expiry issue       | Afternoon  |
| Replace abandoned ORM   | Migrate to Prisma          | 1–2 weeks  |
| Restore test coverage   | Core flows uncovered       | 1 week     |
```

Close with two totals:
- *"To get a working local version: [estimate]"*
- *"To reach production-ready: [estimate]"*

---

**## Where to Start — First 3 Moves**
Three ordered, immediately actionable steps. Written for the person who just
closed this document and opened a terminal.

Not "set up the environment" — that's a category, not a move.
A move is: *"Run `npm install`, expect it to fail on `node-gyp`. Fix:
[exact command]."*

Each step: exact action + what to expect (including likely errors) + why first.

---

**## 30-Day Revival Plan**
Week-by-week, shaped to what was actually found. Part-time pace (evenings +
weekends), not a full-time sprint.

Each week has:
- **Goal** — one sentence on what "done" looks like
- **Key tasks** — 3–5 specific things drawn from the actual findings
- **Watch out for** — the most likely obstacle for this codebase specifically

Arc is always: running → understanding → unblocked → yours.
Contents are specific to this project, not a generic template.

---

**## AI Steering Guide**
For the vibe coder using AI to do the actual revival work. Concrete prompt
patterns for each major area of work — not guidance, actual language.

> **Updating [dependency]:**
> *"Update `[package]` from v[old] to v[new] in `[file]`. Breaking change:
> [specific]. Update all usages in `[affected files]`. Don't touch other deps."*

> **Fixing [broken area]:**
> *"In `[file]`, `[function]` has [specific problem]. Fix it by [approach].
> Don't refactor anything else."*

> **Exploring unfamiliar code:**
> *"Read `[file]` and explain what it does, what it depends on, and what breaks
> if I change [specific thing]."*

This section turns the Revival Document from a report into a working tool.

---

**## Contribution Guide**
For teams, or solo devs who might want collaborators later. Writing it also
forces useful clarity for solo work.

Cover:
- **Setup that works today** — verified against the actual current repo state,
  not the original README which may be broken
- **How to run tests** — exact command, what passing looks like
- **Code conventions** — describe what's actually in the code
- **5 files to read first** — one sentence each
- **Landmines** — what not to touch yet and why. Specific:
  *"Don't modify `src/core/parser.js` — no tests, subtle undocumented behavior"*
- **How to submit changes** — branch conventions, PR expectations

---

**## Open Questions**
Honest gaps. Things the code alone couldn't answer:
- Why was a specific architectural decision made?
- Is there a live deployment for reference?
- Were there plans for unbuilt features?
- Can former contributors be reached for context?

This section isn't a weakness — it's intellectual honesty.

---

## Tone

**Honest but motivating.**

- Name broken things clearly, without catastrophizing:
  *"The ORM needs replacing"* not *"the data layer is a disaster"*
- Surface genuine strengths explicitly — almost every codebase has something
  worth respecting
- Frame effort by what becomes possible:
  *"One focused weekend gets this running"* beats *"setup takes 8 hours"*
- If it genuinely should be rewritten, say so — but explain why and what next
- Address the person making the decision:
  *"You'll want to replace the auth module"* not *"it should be replaced"*

---

## Output

Filename: `revival-[project-name].md`

- With computer tools: write to `/mnt/user-data/outputs/`, call `present_files`
- In chat: deliver as formatted Markdown directly

---

## First-Run Behavior

If triggered without a codebase:

> **Drop any codebase — I'll tell you exactly what you've got.**
>
> - **GitHub link** — `https://github.com/user/repo`
> - **Local folder** — `./my-old-project`
> - **Current directory** — just say "this repo"
>
> I'll read the code, history, issues, and dependencies — then give you one
> document: what still works, what's broken, which path to take, how much work
> it really is, and exactly where to start.
