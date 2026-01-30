---
name: whatamidoing
description: Scan Obsidian vault for uncompleted action items and list them
---

# Obsidian Action Items Scanner

Scan all notes in the Obsidian vault and extract uncompleted action items.

## Vault Location
`/Users/matthew.beltran/Documents/Obsidian Vault`

## Instructions

1. **Find all markdown files**:
   - Use Glob to find all `.md` files: `**/*.md` in the vault path
   - Limit to a reasonable number (e.g., most recent 100 files if too many)

2. **For each file, extract action items**:
   - Read the file
   - Look for uncompleted checkboxes: `- [ ]` followed by text
   - Ignore completed items: `- [x]` or `- [X]`
   - Extract the action item text (everything after `- [ ]`)

3. **Get context for each action item**:
   - Extract the date from:
     - YAML frontmatter `created:` field (preferred)
     - Or parse from filename if format is `YYYY-MM-DD - Title.md`
   - Get the note title (from first `#` heading or filename)
   - Get the section heading the action item is under (if any)

4. **Format and present the results**:
   - Use a grid-style format that groups by date, then note, then section
   - Group items hierarchically to avoid repetition
   - Structure: Date → Note → Section → Tasks
   - Only show file path in a subtle way at the note level, not for each task

   Example format:
   ```
   ## 2026-01-29

   ### Design Review - Sponsorship Installment Promotion
   `Dailies/2026-01-29 - Design Review - Sponsorship Installment Promotion.md`

   **Follow-up Actions**
   - [ ] Follow up with Quin to get concrete answers
   - [ ] Clarify scope and technical approach with sponsorship team

   ### Jawed's Leadership Meeting - PMO Reorganization
   `1v1s/2026-01-28 - Jaweds Weekly Leadership Call.md`

   **Action Items**
   - [ ] Find time to talk to the team
   - [ ] Talk to Flink
   ```

5. **Summary at the end**:
   - Total uncompleted action items found
   - Number of notes with action items
   - Date range covered

## Important Notes
- Only show **uncompleted** items (`- [ ]`)
- Skip completed items (`- [x]` or `- [X]`)
- If there are many items (>50), show the most recent 50 and note how many were skipped
- Sort by date descending (newest first)
- Be concise but informative
