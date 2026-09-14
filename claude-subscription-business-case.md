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

- **dbt and warehouse work:** drafting models, tests, and documentation, and getting up to
  speed in code I didn't write.
- **New processes,** the point I'd push hardest. A process that lives in someone's head gets
  done differently every time. Written as a skill, it becomes a command anyone on the team
  runs the same way, with the same checks. Worth capturing now, while we're still defining them.
- **Recurring reporting:** regenerated from the source data instead of rebuilt by hand each cycle.
- **Internal agents:** bounded reviewers. A QA gate that checks figures against a source of
  truth, or a hygiene agent that flags stale and duplicated records.

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

Cut, in this order: the infrastructure and serving bullets from the pipeline, the recurring
reporting point, then the data-handling section if the director is already past that question.
That leaves about 250 words with the ask intact.

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
