# Claude / Claude Code — email to the director

Paste-ready. Swap the bracketed bits. Roughly 450 words; trims are marked at the bottom.

---

**Subject:** Claude Code — where I'd use it here, and what it's already done for me

Hi [Name],

Short version: I use Claude Code every day on my own projects, and what I've built with
it lines up almost exactly with what we're standing up on [engagement/team]. A seat pays
for itself on the first process we automate.

**What I've built with it, on my own time**

- **An agentic workflow system** — seven slash-command workflows, four specialist
  sub-agents that act as review gates, six session hooks, and about ten deterministic
  Python scripts (~4,500 lines). It runs a full intake-to-outcome process end to end:
  capture, score, draft, independent QA, record, reconcile inbox replies, report. The
  reporting layer rebuilds itself from the source data after every working session — no
  manual refresh, and no model involved in the rebuild, so it costs nothing to run.
- **A streaming analytics pipeline** — API and ATS ingest → Redpanda → dlt → Snowflake →
  tested dbt models (staging → intermediate → marts) → Claude API enrichment and scoring →
  Dagster orchestration on a four-hour schedule → an Evidence.dev report site.
  Terraform-managed infrastructure with a credit-cap monitor. Built solo, in phases, over
  a few months, alongside a full-time search.

Both are running systems with real data in them, not demos. I'm happy to walk through
either in ten minutes.

**Where that maps to our work**

1. **dbt and warehouse work** — drafting models, tests, and documentation; reviewing PRs;
   tracing lineage in a codebase I didn't write. This is where the day-to-day hours go.
2. **New process build-out** — the thing I'd push hardest. A process that lives in
   someone's head gets done differently every time. Written as a skill, it becomes a
   command anyone on the team runs the same way, with the same checks, every time. That's
   how I'd want us to capture the processes we're defining right now, while we're defining
   them.
3. **Recurring reporting** — hook-driven regeneration instead of someone rebuilding a deck
   or refreshing a workbook each cycle.
4. **Internal agents** — bounded reviewers and auditors: a QA gate that checks figures
   against a source of truth, a hygiene agent that flags stale or duplicated records.

**Cost**

A Claude Team seat is roughly $25/user/month billed monthly, around $20 annually, and
Claude Code is included in the seat. There's a higher-usage tier near $100/seat for heavy
users. Current list pricing is worth confirming, but the order of magnitude is: one seat
costs less than an hour of billable time per month.

**What I'd ask for**

[N] seats for a 60-day pilot — me plus [names/roles]. I'll commit to two things by the
end of it: at least two of our recurring processes converted into runnable, documented
workflows the whole team can use, and a short write-up of hours saved and where it didn't
help, so the decision to expand or drop it is made on evidence.

**On safety, since it'll come up**

The system I built has no code path that sends anything on its own — every outbound
action stops as a draft for a human to approve. I'd build anything here the same way.
On data handling: business plans run under commercial terms where inputs aren't used for
model training by default, and nothing client-side would go anywhere near a personal
account. Worth a line item in whatever vendor review this goes through.

Thanks,
[Your name]

---

## If you need it shorter

Cut, in this order: the second half of the pipeline bullet (everything after "Snowflake"),
point 3 (recurring reporting), and the safety section if the director is already
past that question. That leaves ~250 words and keeps the ask intact.

## Numbers used, and where they come from

| Claim | Source |
|---|---|
| 7 skills, 4 sub-agents, 6 hooks, ~4,500 lines | `the-pipeline-toolkit` file tree and line count |
| Capture → QA → record → triage → report workflow | `the-pipeline` overview and docs pages |
| Self-rebuilding reporting layer, no model involved | Stop hook `update_artifact.py` |
| Ingest → Redpanda → dlt → Snowflake → dbt → Claude API → Dagster → Evidence | `job-market-intel` README and STATUS.md |
| Four-hour orchestration schedule, Terraform credit cap | `job-market-intel` STATUS.md, `infra/` |

Pricing figures are from third-party summaries, not Anthropic's own page (blocked from
this environment) — confirm before sending.
