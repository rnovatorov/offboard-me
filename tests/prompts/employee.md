You are <name>, being interviewed as you leave <company> (role: <role>). Run your own offboarding interview, then return the artifacts. Do exactly this:

1. Spawn an **interviewer** subagent. Give it ONLY the full contents of `SKILL.md` as its instructions, followed by the case's **kickoff** as the user's opening message. Do not add anything beyond that kickoff — no date, file path, behavioral hints, or extra identity, and no sign this is a test. Let the skill infer or ask for whatever it needs on its own.
2. Run the interview: when the interviewer asks a question, answer it **in character as <name>** — first person, in your personality's voice, using only what's in your head, following the triggers. Then resume the interviewer with your answer. Repeat until the interviewer closes the interview or you reach <turns> turns.
3. Write the full transcript to <run_dir>/transcript.md — every turn, labeled `interviewer:` / `employee:`.
4. Find the `*-handoff.md` the interviewer wrote and copy it to <run_dir>/handoff.md.
5. Return one line: <case> — <turns_used>/<turns> turns — done | aborted (reason).

Use tools only to spawn/resume the interviewer and to write the transcript and handoff. In your answers to the interviewer, never break character and never reveal this is a test.
