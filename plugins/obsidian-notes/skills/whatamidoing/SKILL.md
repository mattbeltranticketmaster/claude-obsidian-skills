---
name: whatamidoing
description: Scan Obsidian vault for uncompleted action items with filtering by owner, project, or due date
---

# Obsidian Action Items Scanner

Scan all notes in the Obsidian vault and extract uncompleted action items with smart filtering and status indicators.

## Vault Location
`/Users/matthew.beltran/Documents/Obsidian Vault`

## Command Options

**Basic usage:**
```
/whatamidoing
```
Shows all uncompleted action items

**Filter by owner:**
```
/whatamidoing @TianaSmith
/whatamidoing @me
```

**Filter by project:**
```
/whatamidoing project:gco
/whatamidoing {{project:gco}}
```

**Filter by due date:**
```
/whatamidoing overdue
/whatamidoing this-week
/whatamidoing today
```

**Combine filters:**
```
/whatamidoing @TianaSmith project:gco
/whatamidoing overdue @me
```

## Instructions

1. **Parse command arguments**:
   - Extract any filters from ARGUMENTS
   - Owner filter: `@username` or `@me`
   - Project filter: `project:name` or within `{{project:name}}`
   - Date filter: `overdue`, `this-week`, `today`
   - No filters = show all items

2. **Find all markdown files**:
   - Use Glob to find all `.md` files: `**/*.md` in the vault path
   - Limit to most recent 100 files if too many

3. **For each file, extract action items**:
   - Read the file
   - Look for uncompleted checkboxes: `- [ ]` followed by text
   - Ignore completed items: `- [x]` or `- [X]`
   - Parse action item components:
     - Base text (everything before metadata)
     - Owner: `@username` pattern
     - Due date: `#YYYY-MM-DD` pattern
     - Metadata: `{{key:value}}` pattern

4. **Apply filters**:
   - If owner filter: only show items matching that owner
   - If project filter: only show items with matching project metadata
   - If date filter:
     - `overdue`: due date < today
     - `this-week`: due date <= 7 days from now
     - `today`: due date = today

5. **Calculate status for each item**:
   - Get today's date (YYYY-MM-DD)
   - If item has due date:
     - 🔴 Overdue: due date < today
     - 🟡 Due soon: due date within 3 days
     - 🟢 Due later: due date > 3 days
   - If no due date: 🟢
   - Check if stale (note created date > 14 days ago AND no due date)

6. **Get context for each action item**:
   - Extract the date from:
     - YAML frontmatter `created:` field (preferred)
     - Or parse from filename if format is `YYYY-MM-DD - Title.md`
   - Get the note title (from first `#` heading or filename)
   - Get the section heading the action item is under (if any)

7. **Format and present the results**:
   - Group by status first (Overdue → Due Soon → Other)
   - Then by date, then note, then section
   - Use status indicators (🔴 🟡 🟢)
   - Structure: Status → Date → Note → Section → Tasks
   - Show file path subtly at note level

   Example format:
   ```
   # Action Items (15 total)

   ## 🔴 Overdue (2 items)

   ### 2026-01-15 - Design Review - Sponsorship
   `Dailies/2026-01-15 - Design Review.md`

   - [ ] Complete market sign-off @TianaSmith #2026-01-15 {{project:gco, priority:high}}
   - [ ] Review with legal @KarinSparring #2026-01-20 {{project:gco}}

   ## 🟡 Due This Week (5 items)

   ### 2026-01-29 - AU/NZ GCO Weekly Sync
   `Dailies/2026-01-29 - Weekly Sync.md`

   **Follow-up Actions**
   - [ ] Follow up with Quin @MatthewBeltran #2026-02-05 {{project:gco}}
   - [ ] Update Confluence docs @KarinSparring #2026-02-07 {{project:gco}}

   ## 🟢 Future / No Due Date (8 items)

   ### 2026-01-28 - Planning Session
   `Planning/2026-01-28 - Q1 Planning.md`

   - [ ] Research competitor features @TianaSmith {{project:gco}}

   ## ⚠️ Stale Items (>14 days old, 3 items)

   Items with no due date that are over 14 days old:
   - [ ] Talk to Flink (from 2026-01-10)
   - [ ] Schedule retro (from 2026-01-12)
   ```

8. **Summary at the end**:
   - Total uncompleted action items found
   - Breakdown by status
   - Number of notes with action items
   - Date range covered
   - Active filters (if any)

## Important Notes
- Only show **uncompleted** items (`- [ ]`)
- Skip completed items (`- [x]` or `- [X]`)
- If there are many items (>50), show the most recent 50 and note how many were skipped
- Sort by status priority, then date descending (newest first)
- Be concise but informative
- Stale = note older than 14 days AND no due date on the action item
- Status indicators help prioritize work visually

## Filter Examples

**Show only my overdue items:**
```
/whatamidoing @me overdue
```

**Show all GCO project items:**
```
/whatamidoing project:gco
```

**Show Tiana's items due this week:**
```
/whatamidoing @TianaSmith this-week
```

**Show everything (no filter):**
```
/whatamidoing
```
