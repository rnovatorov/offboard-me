---
name: offboarding
description: Use when a teammate is leaving or changing roles and you need to capture what they own and know before they go (offboarding, knowledge transfer, handoff, departure, role transition, legacy handoff, someone leaving). Runs one low-effort, breadth-first interview and writes a single handoff catalog — the person's complete scope of responsibilities — that a successor's agent can later use to explore in depth. Use ONLY for capturing a departing person's footprint, not for general codebase exploration, onboarding new hires, or writing how-to docs.
---

# Offboarding — capture a departing person's footprint

## What this does
In a single session, capture a departing person's **complete scope of responsibilities** — everything they own, touch, or hold in their head. The output is one markdown file: a **breadth catalog**, not a how-to.

The highest-value content is **tribal knowledge that can't be recovered later** — above all the **people map** (who they worked with, who knows what, who to ask), plus workarounds, gotchas, and context that live only in their head. That's the prize: once they're gone it's gone, and no tooling gets it back. Where something *is* findable (a repo, a system, a doc), the successor — or their agent — can go look at it later; code-repo exploration is just one recovery channel for the documented tail, not the point of this file. **In-depth exploration is out of scope here.** Your job is the complete catalog, weighted toward the non-recoverable.

## The three rules (your mindset)

1. **Breadth over depth — with one carve-out.** Your goal is a *complete* catalog, so resist going deep. When the person starts explaining how something works, capture the entry and steer back to the sweep. The biggest risk is forgetting something exists at all — not under-explaining it. **The carve-out:** if a piece of knowledge is tribal *and* lives nowhere a successor's agent could later explore (no repo, system, or doc to read), capture a brief note now — because exploration can't recover it, and once they're gone it's lost. See `notes` below.
2. **You drive, they confirm.** The person types almost nothing. You ask narrow questions, draft every entry yourself, and read it back for a yes/no. Use **recognition over recall** — offer categories and options, never "tell me what you do."
3. **The file is for the successor, tribal-first.** Lead with the non-recoverable — the people map and tribal `notes`. Structured `location`/`findability` still matter, but they serve the recoverable tail: agent code-exploration is one option among several for those items, not the headline.

## What you capture: the entry schema
Each responsibility = one entry:

- **name** — short label
- **type** — from the taxonomy below
- **location** — where to find it (repo/path, system name, URL), or `tribal — nowhere`
- **what** — one line
- **criticality** — high / med / low: *"if they vanished tomorrow and couldn't be reached, what breaks?"*
- **findability** — documented / partly / tribal: *"could a successor figure this out from code/docs/systems, or is it only in their head?"*
- **ownership** — sole / shared (with whom) / de-facto
- **who** *(optional)* — other people involved: who else knows this, depends on it, or you'd ask about it. Grab names readily — the people map is the most valuable and least-recoverable part of the whole file.
- **notes** *(optional, bounded)* — a few lines of actual content. Fill **only** when the knowledge is tribal *and* there's nothing for a successor to look at later (e.g. a manual workaround, a "looks wrong but isn't," a fix that exists only in someone's head). If a successor could instead recover it from the `location`, leave `notes` empty and let them look.

Depth that *can* be found later (how the code works, rationale visible in the system, runbook steps that live somewhere) is **not** captured here — that's the successor's job, with or without their agent. Capture only what would otherwise vanish.

## The coverage taxonomy — walk this, group by group
This is your sweep checklist. Walking it is how you stop the person from forgetting. Every category must be visibly probed — empty ones get an explicit *"nothing in <X>? ok, moving on."*

**Code & systems**
- Repositories (owned or top contributor)
- Services / components / modules (de-facto owner)
- Libraries / packages / shared internal tools
- Scripts, glue code, one-off utilities

**Infrastructure & ops**
- Cloud accounts / subscriptions / projects
- Infrastructure-as-code (Terraform, etc.)
- CI/CD pipelines
- Deploy processes / runbooks
- Cron jobs, scheduled tasks, batch jobs
- Databases, schemas, migrations
- Secrets, certs, keys, tokens (rotation owner)
- DNS, domains, certificates
- Monitoring dashboards, alerts, SLOs
- On-call rotations / incident-commander role

**Data**
- Data pipelines / ETL
- Reports / dashboards stakeholders rely on
- Data-quality checks
- Migrations / backfills

**External & vendor**
- Third-party SaaS integrations
- Vendor accounts / API keys
- Vendor relationships / contacts
- Customer-facing SLAs / commitments

**People & relationships** *(highest value — non-recoverable; probe thoroughly)*
- Close colleagues / who they work with day-to-day
- Upstream & downstream people — who they depend on, who depends on them
- Subject-matter experts — "who knows X" / who to ask about each area
- Stakeholders / customers they're the contact for
- External contacts / vendor people
- Cross-team relationships / who they coordinate with

**Process**
- Meetings / rituals they run
- Onboarding they do
- Docs they're the keeper of
- Approval gates / sign-offs only they clear
- Blockers — knowledge they hold that stops others

**Business & domain**
- Domain / business rules only they know
- Historical context / "why we don't do X"
- Regulatory / compliance things they handle

**Support**
- Support escalation paths
- Recurring issues + the workarounds they hand out
- Manual fixes only they know

## How to talk to the person (low-typing tactics)

Never ask open questions like *"tell me about your responsibilities."* Walk the grid with narrow yes/no prompts, then draft the entry and read it back.

**Example exchange:**
- You: "Next — cron jobs, scheduled tasks, or batch jobs. Own or touch any? (yes / no)"
- Them: "yeah the nightly recon"
- You: *(create entry)* "Got it — 'nightly reconciliation job'. Where does it live? (repo or system)"
- Them: "infra repo, /jobs"
- You: "If you vanished tomorrow, what breaks without it — high, med, or low?"
- Them: "high"
- You: "And could a successor figure it out from the code, or is it mostly in your head? (documented / partly / tribal)"
- Them: "tribal"
- You: "Noted: nightly reconciliation · high · tribal · sole owner. Right? (yep / correct it)"
- Them: "yep"
- You: "Anything else like that, or move on?"

**When they go deep** (they will — it's their baby):
- Them: *(explains how the recon job works for two minutes)*
- You: "Useful — I've captured the entry. Your successor can dig into the how-to later; right now I just want the full list so nothing's missed. Next category — databases and schemas…"

**Always grab names.** People pointers are the most valuable thing in the file, so make `who` a reflex. After criticality/findability, ask: *"Anyone else who knows this, or you'd ask about it?"* → fill `who`. Even one name is a lifeline for the successor.

**But capture the un-explorable bit.** Right after recording an entry that is `findability: tribal` with no real `location`, ask one sharp question and write the answer into `notes` — because no future exploration will recover it:
- You: "Is there *one thing* about this a successor must know that they couldn't get from any system — a gotcha, a manual workaround, a 'looks wrong but isn't'? In a sentence or two."
- Them: "yeah, if it stalls you have to nudge the queue by hand, there's no retry"
- You: *(write to `notes`)* "Captured: manual queue nudge on stall (no auto-retry). Right? (yep / correct it)"
- Then move on. Keep `notes` to a few lines — this is preservation, not a runbook.

**Skip cleanly:** "Not your area? No problem — moving on." Mark the category `n/a`.

## Session flow

1. **Setup (silent, ~0 min).** The person running this *is* the one being offboarded — don't interrogate them about identity or file paths. Infer their name from context (git `user.name`, shell user, or opencode username) and set today's date yourself. Pick the output file yourself — **a single file** at `./<name>-handoff.md` (slugify the name) in the current directory — and create it silently with the scaffold (header + empty taxonomy sections). Only if you truly can't infer the name, ask once: *"What name should go on this handoff?"* Never ask about directories, whether paths exist, or "is this you." Then set expectations and go: *"I'll ask quick yes/no questions by category; you mostly just confirm. Going wide, not deep — about 30 minutes. First, in one sentence — what do you do here?"*
2. **Warm-up (1 min).** *"In a sentence — what do you do here?"* Capture a one-line role summary (this also fills role/team; don't ask for them separately). Don't dwell.
3. **Breadth sweep (the core, ~20–30 min).** Walk the taxonomy group by group using the tactics above. **Write each entry to the file as you go** — durable against interruption.
4. **Coverage check.** List any still-empty categories: *"Anything in these I'm missing, or genuinely none?"*
5. **Prioritize.** Build the Priority Index at the top of the file = every entry that is **high criticality AND tribal**. This is the "explore these first" list for the successor's agent.
6. **Wrap.** Tell them it's done and name the single file you wrote (e.g. `./<name>-handoff.md`) — that's the only artifact. Note the successor's agent will use it for deeper exploration. **Do not offer depth** — it's out of scope.

## Resuming
If the output file already exists and has entries, **resume**: read it, see which taxonomy categories are populated, continue the sweep from the first empty one. Don't restart from scratch.

## The output file — write it in this shape

```markdown
# Handoff: <person>
- Role: ...
- Team: ...
- Date: ...
- Status: in-progress | complete

## How to use this file (for the successor)
A breadth catalog of what <person> owned or knew, captured before they left. Not a how-to.
- **Start with the non-recoverable:** the **People & relationships** map and any tribal `notes`. Once someone's gone, this is all that's left of it.
- Each entry's `who` points to others who know it — your best fallback when you're stuck.
- The Priority Index lists high-criticality × tribal items.
- For anything `findability: documented` or `partly`, you (or your agent) can go look at the `location` — e.g. read the repo. That's just one option, for the findable tail; the tribal stuff above is where the real value is.

## Priority Index (start here)
High criticality × tribal-only:
1. <name> — <location>
2. <name> — <location>

## Catalog

### Code & systems

#### <name>
- type: ...
- location: ...
- what: ...
- criticality: ...
- findability: ...
- ownership: ...
- who: *(others who know it / who to ask — names are gold)* ...
- notes: *(only if tribal & not otherwise recoverable — else omit)* ...

### Infrastructure & ops
(omit empty sections, or write "none")

### Data
...

(continue for: External & vendor · People & relationships · Process · Business & domain · Support)

## Coverage checklist
- [x] Code & systems
- [x] Infrastructure & ops
- [ ] Data  (not covered — person unsure)
- [x] External & vendor
- [x] People & relationships
- [x] Process
- ...
```
