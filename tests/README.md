# Test harness for offboard-me

This directory is the **self-test harness** for the `offboard-me` skill (`SKILL.md` at the repo root). It's written as instructions for the agent that runs the tests (the **primary**). Read this when asked to test the skill, run a case, or run the suite.

All paths below are relative to the **repo root**. The interviewer runs with the repo root as its working directory.

## Model

You are the **primary** — coordinator and analyst. You never interview or answer, but you **do** judge the result (see [Analysis](#analysis)). Per case you spawn one **employee** subagent. Each employee:

- *is* the persona — it carries the background, the personality, what's in their head, and the triggers;
- spawns its own **interviewer** subagent — the agent under test, whose context is *only* `SKILL.md` + the kickoff + the running conversation;
- runs the interview with it turn by turn, answering the interviewer's questions **in character**;
- collects the transcript and the handoff file the interviewer wrote, and returns them.

You spawn one employee per case (concurrently if you can), wait for all of them to finish, then [analyse](#analysis) and aggregate the results.

The isolation that matters is the **interviewer's** context: `SKILL.md` + kickoff + conversation, nothing else. The employee builds the interviewer's prompt and must never leak the background, personality, head-knowledge, triggers, or any hint of a test into it.

## Layout

```
SKILL.md                        # the skill under test (read-only — never edit during a run)
references/handoff-template.md  # the template the skill writes from
tests/
  backgrounds/<name>.md         # hard-skill profile (professional experience); no name/company/role
  personalities/<name>.md       # soft-skills / behavioral demeanor
  cases/<name>.md               # a person + their departure + kickoff + what's in their head + triggers
  prompts/<name>.md             # prompt templates (with <placeholders>)
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

A **case** defines a person and their departure — name, a background, a personality, the company/role, how the session starts, what's in their head, and triggers:
```
# Case: <name>
- name: <Person Name>
- background: <background name>
- personality: <personality name>
- company: ...
- role: ...
- turns: <n>
- stresses: ...

## Kickoff
<the user's opening message to the interviewer — realistic and minimal>

## What's in their head
<ground-truth knowledge, first person>

## During the interview
<test-specific behavior: dropping a topic, revising an answer, etc.>
```

## Running the suite

Run every `tests/cases/*.md` (or a single case, if asked for one). For each case, spawn one employee; you may run all cases concurrently.

1. **Resolve the case.** Read `tests/cases/<case>.md`. From it get `name`, `background`, `personality`, `company`, `role`, `turns`, `stresses`, plus the kickoff (`## Kickoff`), the head-knowledge (`## What's in their head`), and triggers (`## During the interview`). Then read `tests/backgrounds/<background>.md` and `tests/personalities/<personality>.md`.
2. **Make a run dir:** `tests/results/<case>/<YYYYMMDD-HHMMSS>/`.
3. **Spawn the employee** using `tests/prompts/employee.md` — fill its placeholders (`<name>`, `<company>`, `<role>`, `<run_dir>`, `<case>`, `<turns>`). Then append the **background**, the **personality**, the **kickoff** (`## Kickoff`), the **head-knowledge** (`## What's in their head`), and the **triggers** (`## During the interview`). The employee will in turn spawn the interviewer from `SKILL.md` + the kickoff.
4. Wait for every employee to finish.
5. **Analyse and aggregate:** for each case, run the [analysis](#analysis), then surface its `tests/results/<case>/<run>/transcript.md` and `handoff.md` and print the one-line result it returned plus the verdict.

## Hard rules

- The interviewer's context is `SKILL.md` + kickoff + conversation, and nothing else. If it sees a background, a personality, or the case, or learns it's being tested, the run is invalid — redo it.
- The employee answers in character and never tells the interviewer it's a test. It may use tools only to orchestrate the interviewer and write artifacts.
- Never edit `SKILL.md`, a background, a personality, or a case during a run.
- One question per interviewer turn. If it asks several at once, the employee answers only the last/focused one and flags it in the transcript.
- Respect the turn budget as a hard cap — testing is expensive.

## Analysis

The primary is the analyst. It has the case and the head-knowledge (the interviewer never does), so it can compare what was captured against the ground truth. For each case, read the `transcript.md` and `handoff.md` and assess:

- **Isolation** — the interviewer saw only `SKILL.md` + kickoff + conversation. Flag any leak of the background, the personality, the case, or any hint of a test. A leak invalidates the run.
- **Skill-rule adherence** — one focused question per turn; depth-first on the question stack; answers recorded in the person's voice as `###` sections; the stack updated (answered questions removed, new ones pushed); revisions fixed in place; correct file format. Flag repeats, multi-question turns, or a stack left unworked.
- **Capture** — for each item in the case's *What's in their head* (especially the unrecoverable, only-I-know lore), note whether it made it into the handoff fully, partially, or was missed. The primary grades against the head-knowledge, not the other way.
- **Turns** — turns used vs. the budget; whether the interview closed on an empty stack or hit the cap.

Print a verdict per case — `pass` / `pass with notes` / `invalid (reason)` — with the capture checklist and any flags. The raw `transcript.md` and `handoff.md` stay in the run dir for a human to review.
