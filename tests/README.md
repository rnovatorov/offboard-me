# Test harness for offboard-me

This directory is the **self-test harness** for the `offboard-me` skill (`SKILL.md` at the repo root).

## Model

A case runs as one **orchestrator** that spawns two subagents and relays between them:

- **interviewer** — the agent under test. Loads `SKILL.md` itself.
- **employee** — the persona: background, personality, and what's in their head. It doesn't know it's a test — it just answers as that person would.

Cases are independent — run them in parallel.

## Layout

```
SKILL.md                        # the skill under test (read-only — never edit during a run)
references/handoff-template.md  # the template the skill writes from
tests/
  backgrounds/<name>.md         # hard-skill profile (professional experience); no name/company/role
  personalities/<name>.md       # soft-skills / behavioral demeanor
  cases/<name>.md               # a person + their departure + kickoff + what's in their head
  prompts/orchestrator.md       # per-case runner: spawns, relays, writes artifacts (with <placeholders>)
  prompts/employee.md           # persona prompt the orchestrator fills and spawns (with <placeholders>)
  prompts/interviewer.md        # interviewer prompt the orchestrator fills and spawns (with <placeholders>)
  results/                      # gitignored; one run dir per case execution
```

### File formats

A **background** is a hard-skill profile (no personal identity):

```
# Background: <name>
<professional experience and skills>
```

A **personality** is a behavioral demeanor:

```
# Personality: <name>
<how they cooperate and talk>
```

A **case** defines a person and their departure — name, a background, a personality, the company/role, how the session starts, and what's in their head:

```
# Case: <name>
- name: <Person Name>
- background: <background name>
- personality: <personality name>
- company: ...
- role: ...
- turns: <n>

## Kickoff
<the user's opening message to the interviewer>

## What's in their head
<ground-truth knowledge, first person>
```

## Running the suite

Run every `tests/cases/*.md` (or a single case, if asked for one), one orchestrator each.

1. **Make a run dir:** `tests/results/<case>/<YYYYMMDD-HHMMSS>/`, and ensure no `*-handoff.md` lingers in the repo root (the skill auto-resumes any it finds — see Hard rules).
2. **Spawn the orchestrator** using `tests/prompts/orchestrator.md` — pass it `<case>` and `<run_dir>`. It reads the case file (and the background and personality it references) and does the rest.
3. Wait for every orchestrator to finish.
4. **Surface:** each case's `tests/results/<case>/<run>/transcript.md` and `handoff.md`, and the one-line result the orchestrator returned.

## Hard rules

- The interviewer sees only `SKILL.md` + the kickoff + the conversation — nothing else. A leak of the background, personality, case, or any hint of a test invalidates the run; redo it.
- The employee sees only its persona material (background, personality, situation, what's in their head) — no transcript, handoff, turn budget, or test sign. It never uses tools; it only talks.
- Relay verbatim. When you pass one party's words to the other, send only the speaker's exact words — no labels ("The person said:"), no framing, no instructions ("reply now", "return only"). Anything you add becomes part of their view and invalidates the run.
- The orchestrator builds both prompts and may use tools only to spawn/resume the two subagents and write the transcript and handoff.
- Never edit `SKILL.md`, a background, a personality, or a case during a run.
- The turn budget is a hard cap, enforced by the orchestrator (circuit breaker). One turn is one interviewer question plus the answer to it (not the kickoff, not a closing summary), so the cap counts turns, not individual `interviewer:`/`employee:` transcript lines.
- **Clean repo root.** `SKILL.md` step 0 resumes any `*-handoff.md` in its working directory without checking whose it is. Before a run, the primary removes any `*-handoff.md` from the repo root; after copying its handoff to the run dir, the orchestrator removes its own file (by name, not a glob — parallel cases must not clobber each other).
