---
name: saveforlater
description: Automatically capture conversation context and save to Obsidian to resume later
---

# Save Context for Later

Automatically capture the current conversation context and save it to Obsidian so you can resume exactly where you left off.

## Vault Location
`/Users/matthew.beltran/Documents/Obsidian Vault`

## Target Folder
`Resume Later` (will be created if it doesn't exist)

## What This Skill Does

When the user runs `/saveforlater`, you should:

1. **Analyze the current conversation** to extract:
   - Main topic/project being discussed
   - What was accomplished so far
   - Files created, modified, or referenced
   - Key decisions made
   - Current status/blockers
   - Next steps to continue
   - Commands or tools being used
   - Important context needed to resume

2. **Create a comprehensive resume note** with:
   - Clear title based on the topic
   - Structured sections for easy scanning
   - File paths and references
   - Action items and next steps
   - Enough detail to pick up without re-reading the entire conversation

3. **Save to the "Resume Later" folder** with format:
   - Filename: `YYYY-MM-DD - [Topic].md`
   - YAML frontmatter with created date and tags
   - Well-organized markdown content

## Instructions

### Step 1: Analyze the Conversation

Review the recent conversation and extract:
- **Topic:** What is the user working on?
- **Accomplishments:** What have we done so far?
- **Files:** What files were created, read, or modified? Include full paths.
- **Key Decisions:** Any important choices or approaches decided?
- **Status:** Where are we in the process? What's working? What's blocked?
- **Next Steps:** What should happen when the user resumes?
- **Context:** Any other critical information needed to continue?

### Step 2: Generate the Resume Note

Create a well-structured note with these sections:

```markdown
---
created: YYYY-MM-DD
tags: [resume-later, relevant-tags]
---

# [Topic Title]

## Quick Summary
One paragraph overview of what this work is about and current status.

## What We Accomplished
- Bullet list of what was completed
- Include specific outcomes

## Files Created/Modified
List all relevant files with full paths:
- `/full/path/to/file1` - description
- `/full/path/to/file2` - description

## Key Decisions & Approaches
- Important choices made
- Technical approaches decided
- Rationale for decisions

## Current Status
- What's working
- What's not working
- Any blockers or issues

## Next Steps
Ordered list of what to do when resuming:
1. First thing to tackle
2. Second thing
3. etc.

## Important Context
Any other critical information:
- Tools/commands being used
- Dependencies or prerequisites
- Links or references
- Gotchas to remember

## Useful Commands
```bash
# Commands to run when resuming
command1
command2
```
```

### Step 3: Create Folder if Needed

Check if the "Resume Later" folder exists, create if not:
```bash
mkdir -p "/Users/matthew.beltran/Documents/Obsidian Vault/Resume Later"
```

### Step 4: Save the Note

- Generate appropriate filename based on date and topic
- Full path: `/Users/matthew.beltran/Documents/Obsidian Vault/Resume Later/YYYY-MM-DD - Topic.md`
- Save the formatted note

### Step 5: Confirm

Tell the user:
- Where the note was saved
- A brief summary of what was captured
- That they can reference this note to resume later

## Important Guidelines

- **Be comprehensive but concise** - Capture everything needed, but keep it scannable
- **Use absolute file paths** - Makes it easy to find files later
- **Include code snippets** if they're important context
- **Add tags** relevant to the topic for easy searching
- **Focus on resume-ability** - Write it so future-you (or future-Claude) can pick up immediately
- **Don't ask the user for content** - Extract it from the conversation automatically
- **Make it actionable** - Clear next steps, not vague suggestions

## Example Usage

User: `/saveforlater`

You should:
1. Review the conversation
2. Extract all relevant context
3. Generate a comprehensive resume note
4. Save to Resume Later folder
5. Confirm what was saved

The user shouldn't need to provide any additional information - you gather it all from the conversation.
