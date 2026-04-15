# M1 PEO Launch — Full Sync

Syncs all M1 data from Notion, Slack, and Granola into a unified dashboard view. Run anytime for a current snapshot.

## Instructions

### Step 1: Pull Notion M1 Tracker Status

Query the Notion M1 Tracker (`collection://2509dae6-544b-438a-ad13-9cb743eb9b60`) for the following groups (exclude `Phase = 'Key Dates'` from counts):

1. **All rows** — compute totals: Done / In Progress / Blocked / Not Started
2. **Blocked** — `Status = 'Blocked'` — full list with owner + notes
3. **Overdue** — `Status != 'Done'` AND `Target Date < today` — full list
4. **In Progress** — `Status = 'In Progress'` — full list with owner + target date
5. **Due this week** — `Status != 'Done'` AND `Target Date between today and today+7`
6. **Key Dates** — `Phase = 'Key Dates'` AND `Status != 'Done'` — next 5 upcoming by date

### Step 2: Check Slack Channels

1. Read last 15 messages from `#m1peo-dailystandup-ff` (channel ID: `C0ARY03FESU`)
2. Read last 10 messages from `#m1-peo-launch` (channel ID: `C0ANN8JNN03`)
3. Identify: any new blockers, decisions, status updates, or action items mentioned that aren't reflected in Notion

### Step 3: Check Granola for Recent Meeting Notes

1. Use `list_meetings` with `time_range: "this_week"` to find any recent standups or M1 meetings
2. If there are meetings today or yesterday not yet recapped, flag them: "⚠️ {meeting name} — recap pending, run /m1-standup-recap"

### Step 4: Check Action Items & Follow-ups

Query the Action Items & Follow-ups database (`collection://45eea104-610a-478b-a699-11b50a501450`):
- Find any open/not-started action items
- Note any that are overdue based on due date

### Step 5: Output the Sync Dashboard

Print a full dashboard:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📊 M1 LAUNCH SYNC — {date} {time}
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

PROGRESS
  {done}/{total} steps complete ({pct}%)
  ✅ Done: {n}  🟡 In Progress: {n}  🔴 Blocked: {n}  ⬜ Not Started: {n}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🚨 NEEDS ATTENTION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🔴 BLOCKED ({n})
  • {step} — {owner} | {notes}

⚠️  OVERDUE ({n})
  • {step} — {owner} | due {date} ({n} days ago)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🟡 IN PROGRESS ({n})
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  • {step} — {owner} (due {date})

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📅 DUE THIS WEEK
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  • {step} — {owner} (due {date})

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📌 UPCOMING KEY DATES
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  • {milestone} — {date} ({status})

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📋 OPEN ACTION ITEMS ({n})
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  • {owner}: {task} (due {date if set})

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
💬 FROM SLACK (last 24h highlights)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  {1–3 notable updates from Slack not yet in Notion}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚠️  PENDING RECAPS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  {any Granola meetings without a recap — or "All caught up ✓"}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Step 6: Offer Next Actions

After the dashboard, ask:
- "Want me to update any statuses in the Notion tracker?"
- "Want me to run /m1-standup-recap for any pending meetings?"
- "Any action items to log?"
