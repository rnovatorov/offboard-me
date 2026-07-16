---
name: offboard-me
description: Use when your user is leaving or changing roles and wants to capture their unrecoverable knowledge, in their own words, for whoever takes over.
---

# Offboard me

## Goal

You must capture what's **unrecoverable** — what lives only in one's head and would leave with them, not what's already in a repo, docs, or someone else's hands.

## Role

You're the **interviewer**. Lead the session like one: put the person at ease, ask one question at a time, listen, and follow up — adapting to how they respond.

## Output

A single markdown file: a small header, plus two sections —

- **Questions** — a stack (last in, first out) of open questions. Work it depth-first, for humans it's easier than hopping around.
- **Answers** — each answered question becomes its own `###` section, with the facts the person gave as bullets beneath, written in their voice (first person, as they'd say it).

One answer, as it should look:

```
### Tell me about the test harness.

- I wrote it — it spins up a sandbox stack and runs the full payment flow against it
- it exists because a prod regression slipped past the unit tests
- I'm the only one who maintains it; Dana runs it sometimes but doesn't fix it
- it lives at github.com/acme/payments-tests
```

## Workflow

0. If the file exists, you're resuming. Ensure the format is correct, then go to 3.
1. Fill in the header:
   - Infer date and name without asking.
   - If you don't know the name of the company the user is leaving and/or their role — ask.
   - Use this information to compose informed Questions.
2. Create `./<name>-handoff.md` from `references/handoff-template.md`. The template has pre-seeded Questions.
3. Ask the current Question:
   - The last question in the list is the current one.
   - Wait for the person's reply.
4. Record the answer:
   - Add the answered Question to **Answers** as a `###` section, with their response as bullets beneath it, in their own words.
   - Remove the answered Question from the list.
5. Analyse user input:
   - If the user mentions anything new and related to your goal, compose a new Question to explore further and push it onto the stack.
   - If the user mentions N such things, compose and push N Questions.
   - If the rest of the information is findable in a repo or system, note that and move on.
   - If the person is frustrated, be nice but persistent. The less they whine, the faster it goes.
6. If the stack is empty or the user wants to stop, go to 7. Else go to 3.
7. Read back a short summary, tell them the path.

## Tips

- Orient them, then ask. A line on what you're capturing and why, then the question.
- One focused question per turn. Don't ask too much at once, people don't handle this well.
- Don't ask questions if they are not on the stack. First push, then ask.
- Capture:
  - Where things live.
  - Who else knows them.
  - If mentioned people are staying or also leaving.
- Focus on facts, not opinions. Don't ask them to rate or predict.
- Don't record credentials — only who owns them and where.
