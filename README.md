# 🧊 Cold Codebase

> *An archaeologist's kit for abandoned, inherited, and forgotten projects.*

---

## What is it?

Some of the best software in the world is sitting dormant on GitHub. Promising projects that ran out of steam. Tools that solved real problems but lost their maintainer. Codebases handed off between teams without a map.

Cold Codebase is a Claude skill that reads any abandoned or inherited project — code, commit history, open issues, dependencies — and produces one complete **Revival Document** that tells you everything you need to know before touching a single line.

---

## What you get

A single Markdown document covering three things:

**Health Report** — the honest state of the project. What's broken, what's outdated, what's actually still solid. Grouped into Keep / Fix / Replace so there's no ambiguity.

**Revival Plan** — a realistic week-by-week plan for getting the project running and making it yours. Two effort numbers: "just get it running" and "production-ready." Because they're usually very different.

**Contribution Guide** — setup instructions that actually work (not the original README that may be three years out of date), key files to understand, and what not to touch yet.

---

## Who it's for

**The solo dev / vibe coder** who found an interesting abandoned repo and wants to know: is this worth it? How much work is it really? Where do I even start?

**The team that inherited a legacy codebase** — from a previous developer, an acquisition, or just organizational drift. You need a structured assessment you can share and act on immediately.

Both need the same thing: clarity without false hope, and a path forward without overwhelm.

---

## Usage

```
analyze this repo
```
```
I inherited this codebase
```
```
is this worth reviving?
```
```
help me understand what I've got here
```
```
I found an abandoned repo
```
```
this hasn't been touched in years
```
```
I want to pick up where someone left off
```
```
can this codebase be saved?
```

Cold Codebase reads the code, the history, the issues, and the dependencies on its own. It doesn't ask you what it does — it figures that out.

---

## What the output looks like

```
# Revival Document: [Project Name]

  ## The Verdict              ← honest bottom line, 3–4 sentences
  ## Project Snapshot         ← quick-reference table
  ## Recommended Path         ← Maintain / Fork & modernize / Rewrite — and why
  ## What Still Works         ← specific, buildable-on strengths
  ## What's Broken            ← severity + effort per issue
  ## Security Flags           ← critical issues separated from general debt
  ## The Dependency Situation ← Fine / Outdated / Abandoned / Security risk
  ## Effort Estimate          ← work chunks with realistic time ranges
  ## Where to Start           ← 3 concrete first moves, terminal-ready
  ## 30-Day Revival Plan      ← week by week, shaped to this codebase
  ## AI Steering Guide        ← exact prompt patterns for the actual work
  ## Contribution Guide       ← setup that actually works today
  ## Open Questions           ← honest gaps
```

---

## The tone

Balanced — honest but motivating. Broken things are named clearly, without catastrophizing. Genuine strengths are called out. Effort is framed in terms of what becomes *possible*, not just what's required.

Never "this is a disaster." Always "here's what it is, here's what it takes."

---

## File Structure

```
cold-codebase/
└── SKILL.md    ← everything the skill needs, self-contained
```

---

Built by **[Nanasi](https://x.com/oxnanasi)** · [𝕏](https://x.com/oxnanasi) · [GitHub](https://github.com/spellsaif/cold-codebase)

*Because good code deserves a second chance.*
