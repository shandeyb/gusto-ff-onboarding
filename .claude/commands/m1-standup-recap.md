# M1 PEO Launch — Post-Meeting Standup Recap

Run this immediately after the daily standup. Pulls notes from Granola, updates the Notion standup page, logs action items, and drafts the Slack recap.

## Instructions

### Step 1: Find Today's Meeting in Granola

1. Use `list_meetings` with `time_range: "today"` to get today's meetings.
2. Find the standup — look for a meeting with a title containing "standup", "M1", "PEO", or "daily", or the most recent meeting from today.
3. If multiple candidates, show the list and ask which one.
4. Fetch the full transcript/notes using `get_meeting_transcript` with the meeting ID.

### Step 2: Extract Structured Data from Notes

From the Granola transcript/notes, extract:

- **Decisions** — any firm decisions made during the meeting
- **Action Items** — format as `{owner} will {task} by {date if mentioned}`
- **Blockers** — what's stuck and who owns unblocking it
- **Key Updates** — notable status changes, new information, risks raised
- **Discussion highlights** — 2–3 sentence summary of what was talked about

### Step 3: Update Today's Standup Notion Page

1. Search the Daily Standup Log for today's page (title: `YYYY-MM-DD Day — M1 Daily Standup`).
   - Use `notion-query-data-sources` on `collection://a990826d-c0e7-44fa-b3d6-b199569e1473` with title containing today's date.
2. If found, fill in the agenda sections using `notion-update-page` → `update_content`:
   - **Discussion Topics** → discussion highlights
   - **Decisions** → extracted decisions (bullet list)
   - **Action Items** → extracted action items (bullet list)
   - **Blockers / Escalations** → extracted blockers
3. Also populate the **Agenda Prep — Next Session** section:
   - Pull the next 3–5 items due in the next 5 days from the M1 Tracker
   - List any open blockers carrying over
   - Note any decisions pending for next session
   - Format as a ready-to-use agenda for tomorrow's standup

### Step 4: Log Action Items to Notion

For each action item extracted, create a row in the Action Items & Follow-ups database (`collection://45eea104-610a-478b-a699-11b50a501450`):
- Step/title: the task description
- Owner: the person responsible
- Due date: if mentioned
- Status: Not Started

Skip if an identical item already exists.

### Step 5: Draft the Slack Recap

Draft a message for `#m1peo-dailystandup-ff` (channel ID: `C0ARY03FESU`) using this format:

```
:clipboard: *M1 Daily Standup Recap — {date}*

_*Decisions*_
• {decision 1}
• {decision 2}
_(none if no decisions)_

_*Action Items*_
• {owner} — {task} _(by {date if known})_
• ...

_*Blockers*_
• {blocker — owner responsible}
_(none if clear)_

Full notes: {Notion page URL}
```

### Step 6: Present for Review

Show the full drafted recap and ask:
1. "Send this to #m1peo-dailystandup-ff?"
2. "Any edits before sending?"

Do NOT send any Slack message automatically — always get explicit confirmation first.
After confirmation, send via `slack_send_message` to channel `C0ARY03FESU`.
