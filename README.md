# the-pipeline

A job-search operating system built on [Claude Code](https://claude.com/claude-code). It runs my entire search as a single automated workspace: tailoring applications, tracking every lead and submission, sweeping my inbox for recruiter replies, and publishing the live dashboard in this repo.

**Live dashboard:** [drim1561.github.io/the-pipeline](https://drim1561.github.io/the-pipeline/)

The page you see here is a sanitized shared view. Company and contact names from the live pipeline are scrubbed automatically before every deploy; the numbers, stages, and changelog are real.

## What it does

- **Skills (slash commands)** for each phase of the workflow: scaffold a tailored application from a job description, record a submission, triage inbox replies against the tracker, and generate interview prep from a STAR story library.
- **Subagents** that act as quality gates: a job-fit screener that tiers new leads, an application reviewer that checks figure consistency and voice before anything goes out, a company research brief builder, and a tracker auditor.
- **A single source of truth.** One Excel workbook holds the leads inventory and pipeline status. All writes go through two atomic Python scripts with a stage-downgrade guard, so no session can corrupt the tracker.
- **Hooks** that run around every session: a startup briefing that reads the tracker and lists interviews and follow-ups due, warn-only guards for style and file safety, and a stop hook that regenerates this dashboard from the git log and tracker, then deploys it.
- **A candidate-facts config** that keeps every figure identical across resumes, cover letters, and the tracker, plus a voice profile so drafted messages sound like me.

## How this page updates

A Claude Code Stop hook rebuilds the dashboard HTML after every working session: changelog from the project's git history, KPIs and tables from the tracker. It then scrubs company and contact names (a denylist combined with live names read from the tracker itself) and pushes the result here as a single rolling commit.

## Stack

Python (openpyxl, python-docx), Claude Code (skills, subagents, hooks, MCP for Gmail/Calendar/Drive), Excel as the datastore, plain HTML/CSS for the dashboard, GitHub Pages for hosting.

---

Built by [Daniel Rim](https://drim1561.github.io/) · Analytics Engineer · [job-market-intel](https://github.com/drim1561/job-market-intel)
