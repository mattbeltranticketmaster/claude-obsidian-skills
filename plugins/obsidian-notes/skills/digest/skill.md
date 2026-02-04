---
name: digest
description: Generate weekly or daily action item digest with filtering, grouping, and summary statistics
---

# Action Item Digest Generator

Generate comprehensive digests of action items with smart filtering, grouping, and analytics. Perfect for weekly reviews, standups, or personal productivity tracking.

## Vault Location
`/Users/matthew.beltran/Documents/Obsidian Vault`

## Command Options

**Basic weekly digest:**
```
/digest
/digest weekly
```

**Daily digest:**
```
/digest daily
/digest today
```

**Filter by owner:**
```
/digest @TianaSmith
/digest @me
```

**Filter by project:**
```
/digest project:gco
/digest {{project:gco}}
```

**Filter by status:**
```
/digest overdue
/digest this-week
/digest stale
```

**Combine filters:**
```
/digest @me overdue
/digest project:gco this-week
/digest @TianaSmith project:payments
```

**Custom date range:**
```
/digest last-7-days
/digest last-30-days
/digest this-month
```

## Instructions

### Step 1: Parse Command Arguments

1. **Extract filters from ARGUMENTS**:
   - Time range: `daily`, `weekly`, `this-week`, `this-month`, `last-7-days`, `last-30-days`
   - Owner: `@username` or `@me`
   - Project: `project:name` or `{{project:name}}`
   - Status: `overdue`, `stale`, `today`
   - Default: `weekly` if no time range specified

2. **Determine date range**:
   - `daily` / `today`: items for today only
   - `weekly` / `this-week`: next 7 days from today
   - `this-month`: current calendar month
   - `last-7-days`: past 7 days
   - `last-30-days`: past 30 days

### Step 2: Scan and Collect Action Items

1. **Find all markdown files**:
   - Use Glob: `**/*.md` in vault
   - Limit to recent files (e.g., 100 most recent)

2. **Extract all action items**:
   - Look for uncompleted checkboxes: `- [ ]`
   - Parse components:
     - Base text
     - Owner: `@username`
     - Due date: `#YYYY-MM-DD`
     - Metadata: `{{key:value}}`
   - Get context:
     - Note date (from frontmatter or filename)
     - Note title
     - Section heading

3. **Apply filters**:
   - Filter by time range (based on due dates)
   - Filter by owner if specified
   - Filter by project if specified
   - Filter by status if specified

### Step 3: Analyze and Categorize

1. **Categorize by status**:
   - **Overdue**: due date < today (🔴)
   - **Due Today**: due date = today (🟡)
   - **Due This Week**: due date within 7 days (🟡)
   - **Due Later**: due date > 7 days (🟢)
   - **No Due Date**: items without due date (⚪)
   - **Stale**: no due date AND note >14 days old (⚠️)

2. **Calculate statistics**:
   - Total items
   - Count by status category
   - Count by owner
   - Count by project
   - Average age of stale items
   - Completion velocity (if possible)

3. **Identify trends**:
   - Items with most action items (might need breaking down)
   - Owners with most overdue items
   - Projects with most activity

### Step 4: Format Output

Generate a comprehensive digest with this structure:

```markdown
# Action Item Digest - Week of YYYY-MM-DD

**Summary:** [X] total items | [Y] overdue | [Z] due this week | [W] stale

---

## 🔴 Overdue (Y items)

### @TianaSmith (3 items)
- [ ] Complete market sign-off #2026-01-15 {{project:gco, priority:high}}
  📍 From: 2026-01-15 - Design Review
- [ ] Review legal docs #2026-01-20 {{project:gco}}
  📍 From: 2026-01-20 - Weekly Sync
- [ ] Update roadmap #2026-01-25 {{project:payments}}
  📍 From: 2026-01-25 - Planning Session

### @KarinSparring (1 item)
- [ ] Deploy config changes #2026-01-28 {{project:gco}}
  📍 From: 2026-01-28 - Tech Review

---

## 🟡 Due This Week (Z items)

### @MatthewBeltran (2 items)
- [ ] Follow up with Quin #2026-02-05 {{project:gco}}
  📍 From: 2026-01-29 - Weekly Sync
  ⏰ Due in 2 days

- [ ] Review PRs #2026-02-07 {{project:gco}}
  📍 From: 2026-02-03 - Standup
  ⏰ Due in 4 days

---

## ⚠️ Stale Items (W items, >14 days old)

- [ ] Research competitor features @TianaSmith {{project:gco}}
  📍 From: 2026-01-10 - Planning Session
  🕐 24 days old

- [ ] Schedule retro
  📍 From: 2026-01-12 - Weekly Sync
  🕐 22 days old

---

## 📊 Analytics

### By Owner
- @TianaSmith: 5 items (3 overdue)
- @MatthewBeltran: 4 items (0 overdue)
- @KarinSparring: 3 items (1 overdue)
- Unassigned: 3 items

### By Project
- {{project:gco}}: 8 items
- {{project:payments}}: 3 items
- {{project:fraud}}: 2 items
- No project: 2 items

### By Priority
- High: 2 items
- Medium: 5 items
- Low: 1 item
- No priority: 7 items

---

## 💡 Insights

- **Most overdue owner:** @TianaSmith (3 items)
- **Oldest stale item:** "Research competitor features" (24 days)
- **Busiest project:** {{project:gco}} (8 items)
- **⚠️ Attention needed:** 3 items have been stale for >21 days

---

## 🎯 Suggested Actions

1. Review overdue items with @TianaSmith - 3 items need attention
2. Triage stale items - assign owners or close them
3. Consider breaking down "Research competitor features" - it's been open 24 days

---

_Generated: 2026-02-03 10:30 AM_
_Filters: weekly digest, all owners, all projects_
_Sources: 45 notes scanned, 15 action items found_
```

### Step 5: Save Digest (Optional)

1. **Ask user if they want to save the digest**:
   - Use AskUserQuestion
   - Options: "Just show me", "Save to Dailies", "Save to Planning"

2. **If saving**:
   - Filename: `YYYY-MM-DD - Action Item Digest.md`
   - Add YAML frontmatter:
     ```yaml
     ---
     created: YYYY-MM-DD
     tags: [digest, action-items, weekly-review]
     digest_type: weekly
     filters: [filter1, filter2]
     total_items: X
     ---
     ```

## Important Notes

- **Default to weekly view** unless specified otherwise
- **Show context** for each item (which note it came from)
- **Calculate time until due** for items due soon
- **Flag items needing attention** (overdue, very stale)
- **Provide actionable insights** not just data
- **Group intelligently**:
  - Primary grouping by status (overdue first)
  - Secondary grouping by owner
  - Show project tags inline
- **Include analytics section** with statistics
- **Suggest actions** based on patterns identified
- **Support export formats**:
  - Markdown (default)
  - Could support CSV or JSON if requested

## Advanced Features

### Velocity Tracking
If user runs digest regularly, track completion velocity:
- "Last week: 12 items completed, 8 new items added"
- "Net change: -4 items (good progress!)"

### Trend Detection
Identify patterns:
- "Action items for project:gco have increased 30% this week"
- "Stale items have decreased from 8 to 3 - great cleanup!"

### Smart Suggestions
Based on analysis:
- "Consider scheduling a 1v1 with @TianaSmith to discuss overdue items"
- "Project:gco might benefit from a dedicated planning session"
- "3 items have been stale >30 days - archive or assign?"

### Comparison Mode
Compare with previous digest:
```
/digest weekly compare
```
Shows week-over-week changes

## Examples

**Simple weekly digest:**
```
/digest
```
Shows all items due in next 7 days

**My overdue items:**
```
/digest @me overdue
```

**GCO project status:**
```
/digest project:gco
```

**Daily standup digest:**
```
/digest today
```

**Team digest for weekly review:**
```
/digest weekly
```
Full analytics and insights for team review
