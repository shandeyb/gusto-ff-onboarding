# M1 PEO Launch — Morning Standup

Run this before the daily standup to create today's standup page in the Daily Standup Log and prep the agenda.

## Instructions

### Step 1: Pull Current Status from Notion M1 Tracker

Query the Notion M1 Tracker (data source: `collection://2509dae6-544b-438a-ad13-9cb743eb9b60`) for:

1. **In Progress** — `Status = 'In Progress'` AND `Phase != 'Key Dates'`
2. **Blocked** — `Status = 'Blocked'`
3. **Overdue** — `Status != 'Done'` AND `Target Date < today` AND `Phase != 'Key Dates'`
4. **Due in next 5 days** — `Status != 'Done'` AND `Target Date >= today` AND `Target Date <= today+5` AND `Phase != 'Key Dates'`
5. **Recently completed** — `Status = 'Done'` AND `Completed Date >= today-2`
6. **Key Dates** — `Phase = 'Key Dates'` AND `Status != 'Done'` — ordered by Target Date ASC, limit 5

Also compute progress totals: count Done / count all (excluding Key Dates).

### Step 2: Check Slack for Context

1. Read the last 10 messages from `#m1peo-dailystandup-ff` (channel ID: `C0ARY03FESU`) for recent updates and open threads.
2. Read the last 5 messages from `#m1-peo-launch` (channel ID: `C0ANN8JNN03`) for broader team context.
3. Note any action items, blockers, or decisions mentioned.

### Step 3: Create the Standup Page in the Daily Standup Log

Create a new page in the Daily Standup Log database using:
- `parent: { type: "data_source_id", data_source_id: "a990826d-c0e7-44fa-b3d6-b199569e1473" }`
- Title (Date field): `YYYY-MM-DD Day — M1 Daily Standup` (e.g., `2026-04-15 Wed — M1 Daily Standup`)

Page content:

```
# 📊 Tracker Snapshot
Progress: {done}/{total} ({pct}%) — {n} in progress · {n} blocked · {n} overdue

---

## 🟡 In Progress ({count})
| Step | Stage | Owner | Target Date |
|------|-------|-------|-------------|
{rows}

## 🔴 Blocked ({count})
| Step | Owner | Target Date | Notes |
(if none: "None — all clear!")

## ⚠️ Overdue ({count})
| Step | Owner | Due Date | Days Overdue |
(if none: "None overdue!")

## 📅 Due This Week
| Step | Owner | Target Date |
{rows}

## ✅ Recently Completed
| Step | Owner | Completed |
(items Done in last 2 days — if none: "No completions since last standup")

---

## 📌 Next Key Dates
| Milestone | Target Date | Status |
{next 5 key dates}

---

# 🗣️ Today's Agenda

## Discussion Topics
(to be filled during meeting)

## Decisions
(to be filled during meeting)

## Action Items
(to be filled during meeting)

## Blockers / Escalations
(to be filled during meeting)

---

# 📋 Agenda Prep — Next Session
(auto-generated after standup recap — see /m1-standup-recap)
```

### Step 4: Output

After creating the page:
1. Print the Notion page URL
2. Print a brief hot-sheet: top 2–3 items needing attention today
3. Draft this Slack message for review (do NOT send automatically):

```
Good morning team! 🌅 Today's M1 standup agenda is ready:
{Notion URL}

Quick snapshot:
• {n} in progress · {n} overdue · {n} blocked
• 🎯 Focus today: {top 2–3 items}

Add discussion topics to the page before we meet!
```
