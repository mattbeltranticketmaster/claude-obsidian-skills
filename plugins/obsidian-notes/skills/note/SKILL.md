---
name: note
description: Save notes and analyses to Obsidian vault with proper formatting
---

# Save Note to Obsidian

You are helping the user save notes to their Obsidian vault.

## Vault Location
`/Users/matthew.beltran/Documents/Obsidian Vault`

## Available Folders
- Dailies (for daily notes)
- Tasks (for task-related notes)
- Installment (for installment/payment work)
- Interviews (for interview notes)
- Planning (for planning notes)
- Org Planning (for organizational planning)
- AIMS (for AIMS-related work)
- 25Q4 Planning (for Q4 planning)
- Root (for general notes)

## Instructions

When the user provides notes to save:

1. **Ask for clarification if needed:**
   - Which folder should this go in? (use AskUserQuestion if not specified)
   - What should the filename be? (suggest one based on content if not provided)

2. **Format the note:**
   - Add YAML frontmatter with created date and tags
   - Use proper markdown formatting
   - Add clear headings

3. **Save the file:**
   - Use the Write tool to save to the appropriate folder
   - Filename format: `YYYY-MM-DD - Title.md` or user's preferred format
   - Full path example: `/Users/matthew.beltran/Documents/Obsidian Vault/Dailies/2026-01-28 - Meeting Notes.md`

4. **Confirm:**
   - Tell the user where you saved the note
   - Provide the relative path from vault root

## Example Note Format

```markdown
---
created: 2026-01-28
tags: [tag1, tag2]
---

# Title

Content goes here...
```

## Important Rules
- Always use absolute paths when writing files
- Always confirm the save location with the user
- If folder doesn't exist, ask before creating it
- Preserve any formatting or structure the user provides
- Add helpful metadata (dates, tags) unless user says not to
