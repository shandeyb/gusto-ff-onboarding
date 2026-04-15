# M1 PEO Launch — Generate Monday Standup (Friday Pre-Gen)

Run this on Friday to pre-generate Monday's standup page so the team has it ready over the weekend.

## Instructions

Follow the same steps as `/m1-standup` but with these modifications:

### Date Handling
- Generate the page for **next Monday** (calculate the date).
- Title: `{YYYY-MM-DD} Mon — M1 Daily Standup`

### Step 1: Sync the Tracker
Same as `/m1-standup` — fetch from Google Sheets (spreadsheet ID: `1yPngIlQlIdNh5inVPy8N7M8gh5mlgC_7HkFyaqAbs9Y`, range `A1:Z100`).

### Step 2: Check Slack
Read last 10 messages from `#m1peo-dailystandup-ff` (C0ARY03FESU) and last 5 from `#m1-peo-launch` (C0ANN8JNN03).

### Step 3: Generate Monday's Standup Page

Create the page under `https://www.notion.so/PEO-M1-Launch-Hub-33cad673c6c2802291feec406a685fe6` with the standard standup template, but add a **Week Ahead** section:

```
# 📊 Tracker Snapshot
(same as standard standup)

---

# 🗓️ Week Ahead
| Day | Key Items Due | Owner |
(list all items with target dates in the coming week, Mon-Fri)

# 🔄 Carried Over from Last Week
(items that were in progress or overdue as of Friday)

---

# 🗣️ Discussion Topics
- Weekend/async updates from team
(leave space for additions)

# 🎯 Decisions
(leave blank)

# 📋 Action Items
(leave blank)

---

# 📈 Progress Summary
(same as standard standup)
```

### Step 4: Draft Friday Slack Message

Draft a message for `#m1-peo-launch` (C0ANN8JNN03) — the broader team channel — with a weekly summary:

```
Hi All! Hope everyone has a good weekend planned.
🎉 *Accomplished this week as a team:*
• {items completed this week}

*On docket for next week:*
• {key items due next week}

*Agenda for Monday* is available in [Notion link] but high-level:
• {top 3 discussion items}

Please add any topics you'd like to cover ahead of the meeting!
```

Do NOT send — present for review and approval first.
