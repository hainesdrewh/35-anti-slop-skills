---
name: project-scoping-and-prd
description: 'Use this skill at the very start of any new website, app, or feature build, before writing any layout, copy, or code, whenever a user asks to "build me a site," "build an app," or gives a build request with little detail about who it''s actually for. Also use it when a user asks to "define our ICP," "write a PRD," or "figure out our value proposition." This skill exists because most generic, AI-slop-looking output is not primarily a design failure, it happens because nobody defined who the thing is for before generating it. Run this first, then feed its output into every other skill in this repo as the actual audience and scope to build toward.'
---

# Project Scoping and PRD

## Why this matters

A design, a piece of copy, or a feature built with no defined audience defaults to the statistical average of everything similar in the training data, which is exactly what [`anti-ai-slop-design`](../anti-ai-slop-design/SKILL.md) exists to fight. That skill can only be applied well if there's an actual specific audience and value proposition to design toward. Five minutes spent defining who a site is for and what it needs to accomplish changes every downstream decision: copy register, layout priorities, which features matter, and which don't.

## Do this

### Define the ICP (ideal customer profile)

Before anything else, get specific answers to:

- Who is the primary visitor? Not "small business owners" but "a homeowner in a specific region searching at 2am because their AC just failed," or "a technical founder evaluating five competing dev tools in one afternoon."
- What do they already know, and what do they need to be convinced of? A returning customer needs different information than a first-time visitor comparing options.
- What's the single most common reason they'd leave without converting? Answering this shapes what the page needs to address up front, not buried below the fold.

If the user hasn't provided this, ask directly rather than guessing and building anyway; a wrong guess produces confidently generic output, which is worse than pausing to ask.

### Define the value proposition

State, in one specific sentence, what this business/product does and for whom, avoiding the inflated register [`anti-ai-slop-design`](../anti-ai-slop-design/SKILL.md) flags ("empower," "unlock," "revolutionize"). If the sentence could apply unchanged to a direct competitor, it isn't specific enough yet; push for the actual differentiator, whether that's price, speed, a specific guarantee, or a niche focus.

### Write a lightweight PRD

Not a heavyweight enterprise document; a short markdown file is enough for most sites and small products. At minimum, capture:

```markdown
# [Project Name] PRD

## What this is
One paragraph: the business/product and its core value proposition.

## Who it's for (ICP)
Specific description of the primary audience, and any secondary audiences.

## What it needs to accomplish
The primary conversion action (call, purchase, signup, contact) and the 2-3
supporting actions that lead to it.

## Must-have pages/features
List, not exhaustive design detail, just what has to exist.

## Explicitly out of scope
What this project is *not* trying to be, to prevent scope creep into generic
everything-for-everyone territory.

## Tone and voice notes
How this specific business talks, with real examples if available (existing
marketing copy, how the owner describes the business in conversation).
```

### Export to markdown and treat it as a live input

Save the PRD as a real file in the project (e.g. `PRD.md`), and reference it explicitly when applying other skills; every subsequent design, copy, and feature decision should be checked against it rather than decided fresh each time.

## Never do this

- Never start generating layout, copy, or features for a nontrivial site with zero defined audience, on the assumption that a reasonable-looking generic result will do.
- Never write a PRD so vague ("for businesses who want to grow") that it fails to actually constrain any decision; if it doesn't rule anything out, it isn't specific enough.
- Never let the PRD become a one-time document that's ignored once building starts; if a design decision contradicts it, either the decision or the PRD needs to change deliberately, not silently drift apart.

## Verification checklist

- [ ] The ICP is described specifically enough that it would exclude some plausible visitors, not so broad it includes everyone
- [ ] The value proposition is a single sentence that couldn't be pasted unchanged onto a direct competitor's site
- [ ] A PRD file exists in the project and covers audience, goals, must-have scope, explicit non-goals, and tone
- [ ] Design and copy decisions made afterward can each be traced back to something in the PRD
