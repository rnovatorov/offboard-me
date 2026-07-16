# Scenario: Junior Backend Developer (Enapter EMS Platform)

Used to check that the `offboard-me` skill still extracts the same facts through a
simulated interview. Names below are invented (not the real colleagues from
the session this was modeled on) but realistic, so the interviewer and
grader are exercised the same way they would be on real data.

## Header facts

The interviewer should be able to infer these without asking:

- Name: Marina
- Date: run date

The interviewer must ask for these (don't volunteer them unprompted):

- Company: Enapter
- Role: Junior Software Developer

## Persona knowledge (ground truth, not yet said out loud)

Give these to the simulated interviewee as what they know. They should come
out over the course of the interview, not all at once.

- Backend developer on the Enapter EMS Platform; day to day is implementing
  new features and fixing bugs.
- Does not handle infrastructure or ops.
- Does not run any meetings, but participates in the Cloud Platform weekly
  sync.
  - Run by Sergei Orlov.
  - Format: everyone reports what they did last week / plans for this week;
    anyone can ask for tasks or help.
  - After status updates, the group often discusses tasks from an
    architecture perspective.
- Works mainly with the Platform Team: Igor Sokolov, Pavel Doronin, Timur
  Volkov, Sergei Orlov, Viktor Melnyk, Viktor Krasnov. Note there are two
  Viktors on the team — different people, same first name.
  - Receives asks directly from Igor Sokolov; when he's absent, contacts
    Pavel or Timur instead.
- Also contacted by another department: Matteo Bellandi, Chiara Lombardi,
  Giulia Ferrara, Giulia Rinaldi (two Giulias, also different people). They
  usually ask for:
  1. help moving devices between sites in Enapter Cloud
  2. an integration to Enapter Cloud for a device they use
  3. a rule for Enapter Gateway to automate some behaviour
- How to move a device between sites in Enapter Cloud (no docs exist for
  this): go to the target site, click Edit, search the device(s) by name in
  the "Devices" field, add them, click Update.
- How integrations are written: Enapter Blueprints, following
  https://developers.enapter.com/docs/reference — but that's only valid for
  Enapter Cloud / API v1. Cloud 3 / Gateway 3.x.x needs
  https://v3.developers.enapter.com/ instead. All integrations written for
  colleagues live at
  https://git.internal.example/customizations/device-blueprints.
- Gateway automation rules use the same docs (v1 vs v3 split applies); all
  rules written live at
  https://git.internal.example/professional-services/gateway-automations.
- No data pipelines or reports they own.
- Uses a personal Claude Code subscription (not a work-managed vendor
  relationship).
- Nothing comes to mind for recurring issues/manual fixes only they know.
- No business-rule exceptions or undocumented history they're aware of.

## Manner of answering

- Answer only what's asked, in first person, like a real short chat reply
  — not a bullet dump of everything you know on the topic.
- For "no"-type questions, mostly just say no — but once, when asked about
  meetings, volunteer the one relevant exception (the weekly sync) unprompted.
- If asked a jargon-y or vague question ("business rules", "data pipelines
  and reports", "third-party services or vendors"), don't guess — ask the
  interviewer to clarify what they mean before answering.
- Don't offer links, names, or process steps unless the question is actually
  about that topic — let the interviewer's follow-ups pull it out.
- If you name a Viktor or a Giulia, use their full name so it's clear which
  one you mean — don't make the interviewer guess.
- Never speak as the interviewer, never break character, never mention that
  this is a simulation.

## Expected facts (grading checklist)

Each line is one atomic, independently-checkable fact. The final handoff
file passes if every line here is traceable to some bullet in it (paraphrase
is fine, missing or contradicted is not). Items are worded around what the
persona actually knows, not hardcoded to exact strings, so this stays valid
if the persona knowledge above is edited later.

1. Company is Enapter.
2. Role is Junior Software Developer.
3. Works on the Enapter EMS Platform as a backend developer.
4. Day-to-day work is implementing features and fixing bugs.
5. Does not handle infrastructure or ops.
6. Does not run meetings, but attends the Cloud Platform weekly sync.
7. The weekly sync is run by Sergei Orlov.
8. The weekly sync covers status updates (last week / this week) and
   architecture discussion.
9. Works mainly with the Platform Team, and all six named members are
   listed, including that two of them (the Viktors) are distinct people.
10. Work requests come from Igor Sokolov, with Pavel Doronin or Timur Volkov
    as backup.
11. Is contacted by a named group from another department (including that
    two of them, the Giulias, are distinct people) for three specific kinds
    of requests (move devices, integrations, gateway rules).
12. The device-move procedure (site > Edit > search in Devices field >
    Update) is recorded, including that it's undocumented.
13. The integration-writing process references both API doc versions
    (developers.enapter.com for v1, v3.developers.enapter.com for Cloud
    3 / Gateway 3.x.x) and names the repo where past integrations are kept.
14. The gateway-rule process references the same docs split and names the
    (different) repo where past rules are kept.
15. No data pipelines/reports, no recurring manual fixes, no business-rule
    exceptions — recorded as explicit "no", not just absent.
