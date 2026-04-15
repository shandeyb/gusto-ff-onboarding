# M1 PEO Launch — Full Refresh

Recompute all statuses and do a comprehensive audit of the tracker. Use this when data looks off or you want a complete picture.

## Instructions

### Step 1: Full Data Pull

1. Fetch the entire M1 Launch Tracker from Google Sheets (spreadsheet ID: `1yPngIlQlIdNh5inVPy8N7M8gh5mlgC_7HkFyaqAbs9Y`, range `A1:Z100`).
2. Fetch the Notion Launch Hub page (`https://www.notion.so/PEO-M1-Launch-Hub-33cad673c6c2802291feec406a685fe6`) to compare against the Sheet.
3. Read last 20 messages from `#m1peo-dailystandup-ff` (C0ARY03FESU) for recent context.
4. Read last 10 messages from `#m1-peo-launch` (C0ANN8JNN03).

### Step 2: Cross-Reference & Audit

Compare the Google Sheet tracker against the Notion tracker and flag:
- **Status mismatches** — items where Sheet and Notion show different statuses
- **Missing items** — items in one source but not the other
- **Date discrepancies** — different target dates between sources
- **Stale items** — items marked "In Progress" with target dates >5 days past
- **Owner gaps** — items without a clear owner

### Step 3: Compile Full Report

Output a comprehensive report:

```
🔄 M1 Launch — Full Refresh Report ({date})

═══════════════════════════════════════
📊 OVERALL PROGRESS
═══════════════════════════════════════
Total steps: {n}
✅ Done: {n} ({pct}%)
🟡 In Progress: {n} ({pct}%)
⬜ Not Started: {n} ({pct}%)
🔴 Blocked: {n} ({pct}%)

Progress bar: ▓▓▓▓▓▓▓▓░░░░░░░░ {pct}%

═══════════════════════════════════════
🚨 ATTENTION NEEDED
═══════════════════════════════════════

Overdue Items (past target date, not Done):
  1. {step} — {owner} — due {date} ({n} days overdue)
  ...

Blocked Items:
  1. {step} — {owner} — {blocker reason}
  ...

Stale In-Progress (>5 days past target):
  1. {step} — {owner} — target was {date}
  ...

═══════════════════════════════════════
📋 STATUS MISMATCHES (Sheet vs Notion)
═══════════════════════════════════════
  • {step}: Sheet={status}, Notion={status}
  ...
(or "None found — sources are in sync!")

═══════════════════════════════════════
🗓️ KEY MILESTONES
═══════════════════════════════════════
(list all milestones from the KEY DATES section with status)

═══════════════════════════════════════
📅 NEXT 7 DAYS
═══════════════════════════════════════
{date}: {items due}
{date}: {items due}
...

═══════════════════════════════════════
👥 BY OWNER
═══════════════════════════════════════
{owner}: {n} items ({n} done, {n} in progress, {n} not started, {n} blocked)
...
```

### Step 4: Recommendations

Based on the audit, suggest:
1. Items that should probably be escalated
2. Items where status may need updating (e.g., target date passed but still "Not Started")
3. Any patterns or concerns (e.g., one owner has too many concurrent items)
