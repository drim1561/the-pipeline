# Claude / Claude Code — email to the director

Two versions of the same email:

- **`claude-seats-email.html`** — open in a browser, Ctrl+A, Ctrl+C, paste into Outlook.
  Formatting (bold headers, nested bullets, Calibri 11pt) carries over intact.
- **Below** — plain text, for pasting anywhere formatting doesn't survive.

No em dashes anywhere, per the resume-style rulebook.

---

**Subject:** Claude Code: where I'd use it here, and what it's already done for me

Hi [Name],

For my usage, I've used Claude Code pretty heavily on my own projects in the past couple of
months, and what I've built with it lines up almost exactly with what we're standing up.

**What I've built with it, on my own time**

1. **An agentic workflow system**
   - Seven slash-command workflows
   - Four specialist sub-agents that act as review gates
   - Six session hooks and about ten deterministic Python scripts (~4,500 lines)
   - Runs a full intake-to-outcome process end to end: capture, score, draft, independent QA,
     record, reconcile inbox replies, report
   - The reporting layer rebuilds itself from the source data after every working session. No
     manual refresh, and no model involved in the rebuild, so it costs nothing to run.

2. **A streaming analytics pipeline**
   - **Ingest:** public API and ATS sources into Redpanda, loaded to Snowflake with dlt
   - **Modeling:** dbt, staging to intermediate to marts, with tests
   - **Enrichment:** Claude API pulls skills and salary out of free text and scores each record
   - **Orchestration:** Dagster runs the full graph every four hours
   - **Serving:** an Evidence.dev report site
   - **Infrastructure:** Terraform managed, with a credit-cap monitor

Both are running systems with real data in them, built solo and in phases over a few months.

**Where it maps to what we're building here**

- **Getting up to speed, which is where I am now.** The stack works, but it's spread across
  several places and a lot of the business logic only exists inside the views themselves.
  Claude Code reads the actual SQL and traces what depends on what, so a mart view built from
  eight or more stacked CTEs becomes something I can map in an hour instead of an afternoon.
  That's the difference between learning this stack over months and learning it over weeks.
- **Designing the foundational layer.** As the medallion conversations get real, the hard part
  is deciding where the bronze, silver, and gold boundaries fall and what belongs in each. That
  judgment is mine. Everything around it (drafting the model breakdown, the schema files, the
  tests, the naming conventions, and writing it up clearly enough that the team can push back
  on it) is where the hours actually go, and it's where I move several times faster.
- **The migration itself.** Turning existing views into layered models is mostly mechanical
  translation, and it's the bulk of the work. It's also the safest possible use of a model:
  hand it the source view and the target structure, get back the staged models plus tests, then
  verify the new output matches the old view row for row before anything gets swapped. Nothing
  replaces a production object on faith.
- **New processes:** A process that lives in someone's head gets done differently every time.
  Written as a skill, it becomes a command anyone on the team runs the same way, with the same
  checks. Worth capturing now, while we're still defining them.
- **Keeping the foundation from drifting back.** Bounded review agents: one that checks a new
  model against our conventions before it merges, one that flags the same logic implemented in
  two places. A clean architecture degrades the same way the current one did, one reasonable
  shortcut at a time. Automated review is how it stays clean after the migration is done.

**Cost**

A Team seat is roughly $25 per user per month, closer to $20 annually, and Claude Code is
included in the seat. There's a higher-usage tier near $100 for heavy users. Current list
pricing is worth confirming, but the order of magnitude is that one seat costs less than an
hour of billable time a month.

**What I'd ask for**

[N] seats for a 60-day pilot. By the end of it I'd commit to two things: at least two of our
recurring processes converted into documented workflows the whole team can run, and a short
write-up of hours saved and where it didn't help, so expanding or dropping it is an evidence
call.

**On data handling, since it will come up**

The system I built has no code path that sends anything on its own. Every outbound action
stops as a draft for a human to approve, and I'd build anything here the same way. Business
plans also run under commercial terms where inputs aren't used for model training by default.

Thanks,
[Your name]

---

## If you need it shorter

Cut, in this order: the infrastructure and serving bullets from the pipeline, the
drifting-back bullet, then the data-handling section if the director is already past that
question. Keep the first three mapping bullets whatever else goes: they are the ones tied to
work that is actually in front of you.

## Numbers used, and where they come from

| Claim | Source |
|---|---|
| 7 skills, 4 sub-agents, 6 hooks, ~4,500 lines | `the-pipeline-toolkit` file tree and line count |
| Capture → QA → record → triage → report workflow | `the-pipeline` overview and docs pages |
| Self-rebuilding reporting layer, no model involved | Stop hook `update_artifact.py` |
| Ingest, modeling, enrichment, orchestration, serving | `job-market-intel` README and STATUS.md |
| Four-hour schedule, Terraform credit cap | `job-market-intel` STATUS.md, `infra/` |

Pricing figures come from third-party summaries, not Anthropic's own page (blocked from this
environment). Confirm before sending.
