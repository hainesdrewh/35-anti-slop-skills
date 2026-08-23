# Why This Exists

AI tools have made it trivial for anyone to generate a website or an app in minutes. They have not made it easy to generate a *good* one. Left to its own defaults, an AI asked to "build a website" reliably produces the same recognizable output: a purple gradient hero, a three-card feature grid with emoji icons, a fake testimonial carousel, inflated marketing copy, and, underneath the surface, security shortcuts that would never survive a real code review, an unrestricted API key sitting in client-side code, a form with no server-side validation, a login page with no rate limit.

Individually, each of these is a small thing. Together, they produce a site that looks generic on sight and would fail a basic security audit, shipped by someone who had no way to know either of those things was happening, because nothing about the process told them to check.

This repo is an attempt to close that gap directly, by teaching the agent doing the building what a genuinely competent developer already knows and checks for by habit: what makes a design read as templated instead of considered, what SEO fundamentals a launch actually needs, what a real pre-launch checklist covers, and what a backend needs to not be trivially exploitable the week it goes live. Each skill is opinionated on purpose. "It depends" is true of almost everything in software, but a skill that hedges on everything teaches nothing; these are meant to state a clear, defensible default and explain why, so a visitor, a search engine, and an attacker all encounter a site that was actually finished.

And of course, I'm tired of seeing these AI slop websites with no character or purpose. Enough is enough, it's clear everyone thinks they can build a perfect website or a mobile app with Claude or Codex, when in reality they ask one prompt a simple but yet infuriating "Build Me A Website Make It Perfect and No Mistakes" or sometimes maybe a little more but it doesn't matter they all come out the same a blueish purple or darker colored background with some sort of gradient then the next part an annoying header title that has some sort of random color to make it "POP" when in reality they're the most ugly websites known to man now that same person thinks they can become a full time website developer who doesn't even know what a backend is or even a favicon it's just embarrassing. Maybe they watched "Wolf of Wall Street" a few times I mean who wouldn't it's an amazing movie but still they think they can cold call and sell a few websites made by Claude or even sometimes Lovable they all look the same, all so damn ugly and generic. These skills should help with that a lot.

## Who this is for

Anyone using Claude Code (or a similar agent) to build a real site or app and shipping it to actual users and customers, not a disposable demo. That includes people with no traditional development background who are relying entirely on the agent to know what "done" and "safe" actually mean, and it includes experienced developers who want a consistent, checkable standard applied automatically rather than re-explained on every new project.

## What "done" means for a skill in this repo

Every skill states a clear position, names the specific anti-patterns it exists to prevent (calling out the exact tells that make output read as AI-generated, not vague advice to "make it better"), and ends with a concrete verification checklist, something that can actually be checked, not just a reminder to "keep this in mind." A skill that only offers vague best-practice advice with nothing to verify against isn't finished.

## What this repo is not

It's not a replacement for real design taste, a real security review for anything high-stakes, or a lawyer for anything with genuine legal/compliance exposure. It's the baseline that should already be true before any of those bigger conversations happen, so that time spent on real judgment calls isn't spent instead on catching a missing favicon or an unhashed password.
