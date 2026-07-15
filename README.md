# offboard-me

A skill for capturing your own knowledge before you leave a role — so whoever takes over doesn't lose what only lived in your head.

Run it in your last days: one conversational session that **gathers information only** (no analysis, no rating). It walks what you know depth-first, following one topic into the next, and writes a single handoff file made of two lists:

- **Questions** — what's still to ask (works as a stack; the starter questions catch anything you forget).
- **Answers** — what you told it, numbered, in your own words.

Analysis (priorities, risk, who-owns-what) is done separately, later, across handoffs from everyone leaving.

## Use

Clone, then load `SKILL.md` into your agent as instructions (however your agent takes skills or custom prompts), and tell it you're offboarding. It asks you a question, and you're going.

    git clone https://github.com/rnovatorov/offboard-me.git
