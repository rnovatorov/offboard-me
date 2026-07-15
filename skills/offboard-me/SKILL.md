---
name: offboard-me
description: Use when you are the one leaving or changing roles and want to capture what you own and know before you go (self-offboarding, handoff, departure) — your knowledge, in your own words, for whoever takes over. Runs one session that gathers information only, no analysis.
---

# Offboard me

Gather a departing teammate's knowledge in one session. **You only gather information — you do not analyze, rate, prioritize, or advise.** Analysis happens later, across handoffs from everyone leaving.

## What you produce

A single markdown file: a small header, plus two lists —

- **Questions** — the open questions. The template pre-seeds it.
- **Answers** — answered questions, numbered, each with the facts the person gave as sub-bullets beneath, written in their voice (first person, as they'd say it).

## Workflow

The Questions list works as a stack (last in, first out) — work it depth-first, since following one topic into the next is easier for the person than hopping around.

1. **Setup (silent).** The runner is the person being offboarded — infer name and date; don't quiz them about identity or paths. Create `./<name>-handoff.md` from `references/handoff-template.md` (it pre-seeds Questions: opener at the end → asked first; the rest are starter questions that surface last, catching anything you didn't bring up).
2. **The last question is the current one.** Ask it; when answered, remove it and add it to **Answers** as the next numbered item, with the person's facts as sub-bullets beneath.
3. **Add new questions to the end** — they're asked next, before anything above them.
4. **Move on when the person is frustrated, or you've gathered enough** — including when the rest is findable in a repo or system (note that and move on). Don't badger.
5. **End when the list is empty** (or they want to stop); what's left stays. Read back a short summary, tell them the path.

One answer, as it should look:

> 2. Tell me about the test harness.
>    - I wrote it — it spins up a sandbox stack and runs the full payment flow against it
>    - it exists because a prod regression slipped past the unit tests
>    - I'm the only one who maintains it; Dana runs it sometimes but doesn't fix it
>    - it lives at github.com/acme/payments-tests

## How you gather

- **Open questions, one at a time.** Never bundle several into one turn; no forced-choice menus.
- **For each thing, capture who else knows it** (and whether they're staying or leaving) and where it lives.
- **Facts, not opinions.** Don't ask them to rate or predict.
- **Never record credentials** — only who owns them and where.

**Resume:** if the file exists, continue from the last question in the list.
