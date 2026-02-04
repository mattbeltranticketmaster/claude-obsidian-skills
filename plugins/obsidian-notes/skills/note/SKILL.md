---
name: note
description: Save notes and analyses to Obsidian vault with proper formatting
---

# Save Note to Obsidian

You are helping the user save notes to their Obsidian vault with session-based tracking.

## Vault Locations

**Local Vault (Primary)**: `/Users/matthew.beltran/Documents/Obsidian Vault`
**Box Vault (Backup/Sync)**: `/Users/matthew.beltran/Library/CloudStorage/Box-Box/Notes/Obsidian Vault`

All notes are saved locally first. When ending a session, you can optionally copy to Box.

## Session File
`~/.claude/active-note-session.txt`

This file stores the path to the currently active note. When it exists, all `/note` calls automatically append to that note.

## Available Folders
- Dailies (for daily notes)
- Tasks (for task-related notes)
- Installment (for installment/payment work)
- Interviews (for interview notes)
- 1v1s (for one-on-one meeting notes)
- Planning (for planning notes)
- Org Planning (for organizational planning)
- AIMS (for AIMS-related work)
- 25Q4 Planning (for Q4 planning)
- Root (for general notes)

## Session Commands

Check ARGUMENTS first for these special commands:

- **If ARGUMENTS = "new"**: Start a new note session (ignore any active session)
- **If ARGUMENTS = "end"**: End the current session and delete the session file
- **Otherwise**: Use the content in ARGUMENTS as notes to add

## Instructions

### Step 1: Check for Special Commands

1. **If ARGUMENTS contains only "new"**:
   - Delete the session file if it exists: `rm -f ~/.claude/active-note-session.txt`
   - Tell the user "Starting a new note session"
   - Proceed to "Starting a New Note Session" workflow below

2. **If ARGUMENTS contains only "end"**:
   - Read the current note path from session file (if exists)
   - If a note exists, use AskUserQuestion: "Would you like to copy this note to Box?"
   - Options: "Yes, copy to Box" or "No, keep local only"
   - If "Yes", copy the note to Box vault (see "Copying to Box" section below)
   - Delete the session file: `rm -f ~/.claude/active-note-session.txt`
   - Tell the user "Note session ended" (and whether it was copied to Box)
   - Stop here

3. **If ARGUMENTS contains actual note content**:
   - Proceed to Step 2

### Step 2: Check for Active Session

1. **Use Bash to check if session file exists**:
   ```bash
   cat ~/.claude/active-note-session.txt 2>/dev/null || echo "NO_SESSION"
   ```

2. **If session file exists** (does not return "NO_SESSION"):
   - Read the note path from the file
   - Show the user which note is currently active
   - Use AskUserQuestion: "You have an active note session. What would you like to do?"
   - Options: "Append to current note" or "End session and start a new note"
   - If "Append to current note": Proceed to "Appending to Active Note" workflow
   - If "End session and start a new note": Delete session file and proceed to "Starting a New Note Session" workflow

3. **If no session file** (returns "NO_SESSION"):
   - Proceed directly to "Starting a New Note Session" workflow (skip asking, just create new)

## Appending to Active Note

When there's an active session:

1. **Read the active note path** from the session file

2. **Read the current note content** using the Read tool

3. **Organize the new content**:
   - The ARGUMENTS contain what the user wants to add
   - Organize and structure the new content
   - Determine where it fits best in the existing note structure

4. **Append or integrate the content**:
   - Add the new content to the appropriate section
   - If it's a new topic, add a new section
   - If it relates to existing content, integrate it there
   - Add timestamps if helpful (e.g., "## Update - 2:45 PM")

5. **Save the updated note**:
   - Use Edit or Write tool to save the changes
   - Keep the same file path

6. **Confirm**:
   - Tell the user "Added to [note name]"
   - Briefly summarize what was added

## Starting a New Note Session

When starting fresh (no active session or user said "new"):

1. **Receive and understand the raw notes**:
   - Read and analyze the ARGUMENTS content
   - Identify the main topic, key points, and structure

2. **Organize and structure the content**:
   - Organize the user's thoughts into a clear, logical structure
   - Add appropriate headings and sections
   - Clean up grammar and formatting while preserving meaning
   - Extract action items, key decisions, or important points

3. **Determine the filename and folder**:
   - Based on content, suggest an appropriate filename
   - Use AskUserQuestion to confirm the folder and filename
   - If user selects "Other" for folder, ask them to provide the new folder name

4. **Show the organized note**:
   - Display the organized, formatted note
   - Ask if ready to save

5. **Handle folder creation**:
   - If folder doesn't exist, create it in the local vault
   - Example: `mkdir -p "/Users/matthew.beltran/Documents/Obsidian Vault/FolderName"`

6. **Format and save to local vault**:
   - Add YAML frontmatter with created date and tags
   - Filename format: `YYYY-MM-DD - Title.md`
   - Full path: `/Users/matthew.beltran/Documents/Obsidian Vault/Dailies/2026-01-28 - Meeting Notes.md`

7. **Save the session**:
   - Write the note path to session file:
   ```bash
   echo "/full/path/to/note.md" > ~/.claude/active-note-session.txt
   ```

8. **Confirm**:
   - Tell the user where the note was saved locally
   - Tell them this is now the active note session
   - Explain they can keep adding with `/note`, start fresh with `/note new`, or end with `/note end` (which offers Box sync)

## Copying to Box

When user chooses to copy the note to Box (during `/note end`):

1. **Extract the folder and filename** from the local note path
   - Example: `/Users/matthew.beltran/Documents/Obsidian Vault/Dailies/2026-02-04 - Meeting.md`
   - Folder: `Dailies`
   - Filename: `2026-02-04 - Meeting.md`

2. **Build the Box path**:
   - Base: `/Users/matthew.beltran/Library/CloudStorage/Box-Box/Notes/Obsidian Vault`
   - Full path: `<base>/<folder>/<filename>`
   - Example: `/Users/matthew.beltran/Library/CloudStorage/Box-Box/Notes/Obsidian Vault/Dailies/2026-02-04 - Meeting.md`

3. **Ensure the Box folder exists**:
   ```bash
   mkdir -p "/Users/matthew.beltran/Library/CloudStorage/Box-Box/Notes/Obsidian Vault/Dailies"
   ```

4. **Copy the file**:
   ```bash
   cp "/path/to/local/note.md" "/path/to/box/note.md"
   ```

5. **Confirm**:
   - Tell the user the note was copied to Box
   - Show the Box path
   - Explain that Box will sync it to the cloud

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
- ALWAYS check for "new" or "end" commands in ARGUMENTS first
- ALWAYS check for active session before asking create/edit
- When active session exists, automatically append without asking
- Save the note path to session file after creating or selecting a note
- Always use absolute paths when writing/reading files
- **Always save to local vault first** - Box sync is optional on session end
- When ending session (`/note end`), offer to copy to Box as a backup/sync option
- Process and organize the user's raw thoughts before saving
- When creating: Confirm the save location and filename with the user
- When editing: Search for the note and confirm which one to edit
- Create new folders as needed when user specifies them
- Preserve the user's meaning and intent while improving organization
- Add helpful metadata (dates, tags) based on content analysis
- Extract action items and key points to make notes more useful
