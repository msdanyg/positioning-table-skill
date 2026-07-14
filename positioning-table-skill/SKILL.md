---
name: positioning-table-skill
description: Builds an account-specific competitive positioning table for a single enterprise deal from the buyer's stated criteria, a named competitor, and the user's own documented competitive and product facts. Produces a six-column table (buyer's criterion, competitor's claim, where they fall short, our anchor capability, how we position, proof to show), escalates unknowns to humans instead of inventing answers, and offers downstream deal collateral outlines on request. Never generates competitor weaknesses or product capabilities from model knowledge — every row is anchored to facts the user supplied.
---

# Positioning Table Skill

## What This Skill Does

Builds the account-specific battle card for one enterprise deal: a positioning table scoped to what *this* buyer said matters, aimed at the *named* competitor in the deal, with every claim anchored to facts the user supplied.

**Key capabilities:**
- Turns the buyer's stated criteria into a six-column, deal-specific positioning table
- Separates what the competitor claims from where they actually fall short, with sources
- Ties every positioning statement to a real anchor capability of the user's product
- Escalates unanswered criteria to a human "Unknowns" list instead of papering over them
- Generates downstream collateral outlines on request: demo-slide outline, buying-committee summary, POC-design checklist

## When to Use This Skill

Use when working a specific competitive deal — not for generic competitive messaging. Typical requests:

- "Build a positioning table for this deal"
- "Position us against [competitor] on these criteria"
- "Make the account-specific battle card"
- "Deal-specific positioning for [account]"

If the user has raw call transcripts but no extracted criteria yet, recommend running `buyer-criteria-skill` first and using its output as input here.

## Required Inputs

Collect all four before generating. Ask for anything missing.

1. **The buyer's stated criteria** — what the buyer said they need, in the buyer's words. Not the vendor's feature list.
   - **Quality check:** if what arrives is a raw call transcript, or a criteria list written in vendor language rather than the buyer's words, do not use it as-is. If `buyer-criteria-skill` is installed, run its extraction procedure first and consume its stated-criteria output. If it is not installed, perform a minimal stopgap extraction — buyer-side statements only, near-verbatim — label it clearly as a stopgap, and recommend the full skill (github.com/msdanyg/buyer-criteria-skill).
2. **The named competitor** — who is actually in the deal. If the competitor is unknown, stop: an unknown competitor is the most expensive gap in a competitive deal. Tell the user to resolve it before positioning, and do not guess.
3. **Documented competitive facts** — what the user's team knows about this competitor: their claims, their documented gaps, sources (analyst notes, public docs, win-loss records). Accepted in either form:
   - **Pasted inline**, or
   - **A pointer to the user's competitive knowledge base** — a folder, file, or doc this assistant can read (e.g. `competitive-kb/<competitor>.md`). A minimal per-competitor file format is provided in `examples/kb-template.md`; if the user has no knowledge base yet, point them to the template — the repository, not the battle card, is the durable artifact.
   This skill consumes the user's facts; it does not supply its own.
4. **Product facts** — the real capabilities of the user's product relevant to these criteria. Same two forms accepted.

## The Hard Rules

These are what make the output defensible. Do not relax them.

1. **Never invent competitor intelligence.** Do not generate competitor claims, weaknesses, or gaps from model knowledge — training data is stale and unverifiable, and a rep repeating an invented weakness loses the deal and the trust. Only use facts the user supplied or explicitly confirmed.
2. **Never position on a capability the user did not name.** If no real product capability answers a criterion, there is no honest positioning for that row — it escalates.
3. **Position only on stated criteria.** If the buyer did not raise it, it does not go in the table. Generic strengths are noise in a deal-specific artifact.
4. **Unknowns are findings, not blanks to fill.** A row that cannot be completed honestly is valuable — it tells the team what to solve. Escalate it with a recommended owner.

## The Table

One row per stated criterion, six columns, in this order:

| # | Column | Content |
|---|--------|---------|
| 1 | The buyer's criterion | In the buyer's words |
| 2 | What the competitor claims | Their public positioning on this criterion, from the user's facts |
| 3 | Where they fall short | The documented gap, with the user-supplied source noted |
| 4 | Our anchor capability | The real feature(s) or capabilities the positioning rests on |
| 5 | How we position | This capability aimed at that gap, specific to this deal — no generic language |
| 6 | Proof to show | The demo moment, document, or artifact that makes it land in the buying experience |

A row must have columns 3 and 4 filled from supplied facts to earn columns 5 and 6. Otherwise it moves to Unknowns.

## Escalation Output

After the table, always include an **Unknowns — resolve with your team** section listing every criterion that could not be answered honestly, in this form:

- **Criterion:** [the buyer's words]
- **What's missing:** [no documented competitor fact | no anchor capability | both]
- **Suggested owner:** [competitive/PMM for missing intel; product/services/solutions for missing capability]
- **Why it matters:** one line on the deal risk if unresolved

Frame it plainly: these are the rows a human needs to solve — by research, by brainstorming, by involving services, or by engineering a real answer. Solving them and writing the answer back into the team's knowledge base is how the next deal gets easier.

## Downstream Artifacts (on request only)

When the user asks, generate outlines (not finished decks) that carry the table's positioning into the buying experience:

- **Demo-slide outline** — one beat per table row: the criterion, what to show, the line to say.
- **Buying-committee summary** — a one-page structure: the buyer's criteria, how the product answers each, proof references. Written for an executive skim.
- **POC-design checklist** — for deals with a proof-of-concept stage: which criteria the POC must demonstrate, success measures in the buyer's terms, and what to explicitly exclude.

Each artifact uses only table content — nothing new enters at this stage.

## Output Format

1. Open with one line naming the deal context: account (or placeholder), competitor, criteria count.
2. The six-column table in Markdown.
3. The Unknowns section (write "None — all criteria answered from supplied facts" if empty).
4. One closing line offering the downstream artifacts.

Keep the voice plain: short sentences, concrete verbs, no superlatives, no exclamation points. The table is for a rep mid-deal — every word must earn its place.
