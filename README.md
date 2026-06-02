# Test-cursor-security-automation

Security intelligence automation for hourly threat collection and daily synthesis.

## Overview

Two Cursor automations work together in a map-reduce pattern:

| Automation | Schedule | Prompt | Output |
|------------|----------|--------|--------|
| Hourly Security News Check | Every hour (`0 * * * *` UTC) | [prompts/hourly-security-check.md](prompts/hourly-security-check.md) | Per-hour tactical intel report |
| Daily Security Intelligence Review | Daily at 23:55 UTC (`55 23 * * *`) | [prompts/daily-security-review.md](prompts/daily-security-review.md) | End-of-day executive brief |

The hourly agent discovers and validates intelligence from external sources. The daily agent reads all hourly reports, deduplicates findings, detects escalations, and produces a single ranked remediation brief.

## Repository Layout

Reports are stored under `reports/{YYYY}/{MM}/{DD}/`:

```
reports/
  2026/
    06/
      02/
        00/
          security-intel-report.md       # hourly
        01/
          security-intel-report.md
        ...
        23/
          security-intel-report.md
        daily/
          security-intelligence-daily-brief.md   # daily synthesis
        index.json                               # optional metadata index
```

### Path Conventions

- **Hourly reports:** `reports/{YYYY}/{MM}/{DD}/{HH}/security-intel-report.md`
- **Daily briefs:** `reports/{YYYY}/{MM}/{DD}/daily/security-intelligence-daily-brief.md`
- **Hour format:** Two-digit UTC hour (`00`–`23`)
- **Date format:** Four-digit year, two-digit month, two-digit day

### Report Metadata

Both report types include YAML front matter for programmatic parsing:

- Hourly reports include `new_since_last_hour` and `ongoing_from_earlier_today` blocks for delta framing.
- Daily briefs include `hourly_reports_ingested`, `hourly_reports_missing`, and aggregated severity counts.

See the prompt files for the full front matter schemas.

## Setting Up Cursor Automations

1. Create an automation named **Hourly Security News Check**:
   - Schedule: `0 * * * *` (every hour, UTC)
   - Agent prompt: contents of [prompts/hourly-security-check.md](prompts/hourly-security-check.md)
   - Connect to GitHub repo: `dfalt0/Test-cursor-security-automation`

2. Create an automation named **Daily Security Intelligence Review**:
   - Schedule: `55 23 * * *` (23:55 UTC daily)
   - Agent prompt: contents of [prompts/daily-security-review.md](prompts/daily-security-review.md)
   - Connect to GitHub repo: `dfalt0/Test-cursor-security-automation`

Schedule definitions are also in [automation/schedules.yaml](automation/schedules.yaml).

## GitHub Actions (Optional)

Workflow files in `.github/workflows/` mirror the same schedules for visibility and manual triggering via `workflow_dispatch`. They document expected run times and can be extended to integrate with external triggers.

## Commit Messages

- Hourly: `hourly: {YYYY-MM-DD} {HH}:00 UTC security intel report`
- Daily: `daily-review: {YYYY-MM-DD} security intelligence brief`
