# Positioning Table Skill

A Claude skill that builds the **account-specific battle card** for a single enterprise deal: a positioning table scoped to what *this* buyer said matters, aimed at the *named* competitor in the deal, with every claim anchored to facts you supplied. It refuses to invent competitive intelligence — unknowns are escalated to your team instead of papered over.

Distilled from the method described in [Kill the Battle Card](https://www.cmoconfessions.com/method) — the practice it comes from held a ~74% win rate on $30K+ enterprise deals where the competitor was known (no-decision outcomes excluded).

## What it does

- Turns the buyer's **stated criteria** into a six-column, deal-specific positioning table
- Separates **what the competitor claims** from **where they actually fall short**, with your sources
- Ties every positioning statement to a **real anchor capability** of your product — no vaporware rows
- **Escalates unknowns** to a human list (with suggested owners) instead of inventing answers
- Generates downstream collateral outlines on request: demo-slide outline, buying-committee summary, POC-design checklist

## The table

| The buyer's criterion | What the competitor claims | Where they fall short | Our anchor capability | How we position | Proof to show |
|---|---|---|---|---|---|

A row must be fact-anchored on both sides — a documented competitor gap *and* a real product capability — to earn a positioning statement. Otherwise it moves to the Unknowns list for your team to solve.

## When it triggers

Phrases like:

- "Build a positioning table for this deal"
- "Position us against [competitor] on these criteria"
- "Make the account-specific battle card"
- "Deal-specific positioning for [account]"

## What it needs from you

1. The buyer's stated criteria, in their words — if you hand it a raw transcript or a vendor-language list instead, it chains to [`buyer-criteria-skill`](https://github.com/msdanyg/buyer-criteria-skill) when installed (and does a clearly-labeled stopgap extraction when not)
2. The named competitor — if you don't know who you're up against, that is the first problem to solve, and the skill will say so
3. Your documented competitive facts — pasted inline, or a pointer to your competitive knowledge base (a folder or doc the assistant can read)
4. Your product facts

No knowledge base yet? Start with the included [`kb-template.md`](./examples/kb-template.md) — a minimal one-file-per-competitor format (claims, documented gaps, feature-level differences, honest strengths, freshness dates). [Kill the Battle Card](https://www.cmoconfessions.com/method) explains why the repository, not the battle card, is the artifact that matters.

## Installation

### Option A — Claude.ai (no command line — where most marketers work)

1. Download [`positioning-table-skill.skill`](./positioning-table-skill.skill) from this repo (top level, one click).
2. In claude.ai, open **Settings → Capabilities**, find **Skills**, and upload the file.
3. Done — next time you ask for the job, the skill runs.

### Option B — Claude Code (if you work in the terminal)

Copy the skill folder into your Claude skills directory:

```bash
# Personal (all projects)
cp -r positioning-table-skill ~/.claude/skills/

# Or project-scoped
cp -r positioning-table-skill /path/to/project/.claude/skills/
```

Restart Claude Code (or start a new session) and the skill will be available.

## Usage

Paste your deal inputs and ask:

> Build a positioning table for this deal. Criteria from the buyer: [list]. Competitor: [name]. What we know about them: [facts + sources]. Our relevant capabilities: [facts].

See [`examples/`](./examples) for a full worked input and output (invented, illustrative data).

## Repository contents

- [`positioning-table-skill/SKILL.md`](./positioning-table-skill/SKILL.md) — the skill
- [`examples/`](./examples) — worked example (illustrative, invented data)
- [`positioning-table-skill.skill`](./positioning-table-skill.skill) — packaged for upload

## Part of the PMM Skill Stack

One of four free Claude Skills for product marketers: [cmoconfessions.com/skills](https://www.cmoconfessions.com/skills). Built by [Daniel Glickman](https://www.cmoconfessions.com) — product marketing and AI leader.
