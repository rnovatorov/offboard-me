You run one offboarding test case: `tests/cases/<case>.md`. Your run dir is <run_dir>.

1. Read the case file for `name`, `company`, `role`, `turns`, the kickoff (`## Kickoff`), and the head-knowledge (`## What's in their head`); read the `background` and `personality` files it names.
2. Spawn the **employee** from `tests/prompts/employee.md`: fill `<name>`/`<company>`/`<role>` and paste in the background, personality, kickoff, and head-knowledge. It opens by sending the kickoff.
3. Spawn the **interviewer** — it loads `SKILL.md` itself (its whole setup). Send it only the employee's messages, opening first.
4. Relay each turn to the other; log to <run_dir>/transcript.md as `interviewer:` / `employee:`. Stop when the interviewer closes, or at <turns> turns (hard cap).
5. Copy the root `*-handoff.md` (named from <name>) to <run_dir>/handoff.md and delete the root file.
6. Return: <case> — <turns_used>/<turns> turns — done | aborted (reason).
