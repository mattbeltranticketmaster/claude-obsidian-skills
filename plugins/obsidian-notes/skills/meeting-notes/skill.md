---
name: meeting-notes
description: Parse meeting transcripts and generate structured summaries with decisions, actions, and smart tagging
---

# Meeting Notes Intelligence

Parse meeting transcripts or notes from various sources and generate structured, searchable meeting summaries with automatic action item extraction.

## Vault Location
`/Users/matthew.beltran/Documents/Obsidian Vault`

## Supported Input Sources

1. **Raw text from user**
   - User provides meeting notes as ARGUMENTS
   - Can be rough notes, bullet points, or narrative

2. **Confluence meeting notes**
   - User provides Confluence URL
   - Fetch using MCP Confluence tools

3. **Microsoft Teams transcripts**
   - User provides Teams meeting URL or transcript
   - Fetch using MCP Microsoft Graph tools

4. **Existing markdown file**
   - User provides path to existing meeting notes
   - Read and restructure

## Meeting Note Structure

Generate notes with this structure:

```markdown
---
created: YYYY-MM-DD
tags: [meeting, <meeting-type>, <project-tags>]
meeting_date: YYYY-MM-DD
meeting_time: HH:MM (optional)
attendees: [Name1, Name2, Name3]
meeting_type: <type>
---

# <Meeting Title> - YYYY-MM-DD

## Context
Brief 2-3 sentence summary of what the meeting was about and why it happened.

## Decisions
- **Decision 1**: Clear statement of what was decided
- **Decision 2**: Another decision with rationale if needed

## Discussion Points

### Topic 1
Notes about the discussion, key points raised, concerns, questions

### Topic 2
More discussion notes organized by topic

## Action Items
- [ ] Action description @Owner #YYYY-MM-DD {{project:name, priority:level}}
- [ ] Another action @AnotherOwner #YYYY-MM-DD {{project:name}}

## Follow-ups / Open Questions
- Outstanding question 1 that needs resolution
- Follow-up item that doesn't have an owner yet
- Dependency on another team

## Notes / Additional Context
Any other relevant information, links, references
```

## Instructions

### Step 1: Get Input

1. **Check ARGUMENTS for input source**:
   - If it's a URL (Confluence or Teams), fetch the content
   - If it's a file path, read the file
   - If it's raw text, use it directly
   - If ARGUMENTS is empty, ask user to provide meeting notes

2. **Fetch from external sources if needed**:
   - Confluence: Use MCP Confluence tools to fetch page content
   - Teams: Use MCP Microsoft Graph tools to fetch transcript
   - Handle errors gracefully if fetching fails

### Step 2: Parse and Structure

1. **Extract meeting metadata**:
   - Meeting title/topic
   - Date (from content or ask user)
   - Attendees (extract names mentioned or ask user)
   - Meeting type (infer or ask):
     - `weekly-sync`, `standup`, `planning`, `retro`, `1v1`
     - `all-hands`, `design-review`, `tech-review`, `kickoff`

2. **Identify key sections**:
   - **Decisions**: Look for keywords like "decided", "agreed", "approved", "will do"
   - **Discussions**: Main topics covered, organized by theme
   - **Action items**: Look for:
     - "TODO", "Action item", "Follow up"
     - Statements with owners: "X will do Y"
     - Deadlines: "by Friday", "next week", specific dates
   - **Open questions**: "?", "unclear", "need to figure out", "TBD"

3. **Extract action items**:
   - Parse owner from context (who's responsible)
   - Extract or infer due dates
   - Add project tags based on meeting context
   - Format: `- [ ] Task @Owner #due-date {{metadata}}`

### Step 3: Smart Tagging

1. **Auto-assign meeting type tag**:
   - Analyze meeting title and content
   - Common patterns:
     - Contains "1:1" or "1v1" → `1v1`
     - Contains "weekly", "sync" → `weekly-sync`
     - Contains "standup", "daily" → `standup`
     - Contains "planning" → `planning`
     - Contains "retro", "retrospective" → `retro`

2. **Auto-assign project tags**:
   - Extract from meeting title or content:
     - "GCO" → `gco`
     - "Payments", "TM Payments" → `payments`
     - "Fraud" → `fraud`
     - "AU", "NZ", "Australia" → `aunz`
   - Ask user to confirm/add tags

3. **Auto-assign priority to action items**:
   - Keywords indicating high priority:
     - "urgent", "ASAP", "critical", "blocker", "immediately"
   - Keywords indicating medium priority:
     - "soon", "this week", "important"
   - Default to no priority tag if unclear

### Step 4: Save and Confirm

1. **Show the structured note to user**:
   - Display the full formatted meeting note
   - Highlight action items extracted
   - Show auto-assigned tags

2. **Ask for confirmation**:
   - Use AskUserQuestion to confirm:
     - Meeting title
     - Folder location (default: Dailies)
     - Tags
     - Attendees
   - Options for folder: Dailies, 1v1s, Planning, Org Planning, Other

3. **Save the note**:
   - Filename format: `YYYY-MM-DD - <Meeting Title>.md`
   - Use Write tool to save to chosen folder
   - Confirm to user where it was saved

4. **Summary response**:
   - "✓ Saved meeting notes: [Title]"
   - "📍 Location: [Path]"
   - "📝 Extracted [X] action items"
   - "🏷️ Tags: [tag list]"

## Important Notes

- **Extract all action items automatically** - don't require manual identification
- **Infer owners from context** - "John will review" → `@John`
- **Guess due dates when possible**:
  - "by Friday" → calculate next Friday
  - "next week" → 7 days from meeting date
  - "end of month" → last day of current month
- **Preserve original meeting content** in Discussion Points
- **Don't lose information** - if something doesn't fit a category, put it in Notes
- **Auto-tag but allow user override** before saving
- **Be smart about parsing formats**:
  - Handle bullets, numbers, paragraphs
  - Extract from narrative text
  - Handle poorly formatted notes

## Examples

**Input (raw text):**
```
GCO AU/NZ Weekly Sync - Feb 3

Tiana, Karin, Matt attended

We decided to move forward with the Exchange/Upgrade solution for Q4.
This unblocks scaling to 100%.

Matt will follow up with Quin about the timeline by Feb 10.
Karin needs to update the Confluence docs this week.

Still need to figure out the Booking Protect integration timeline.
```

**Output (structured):**
```markdown
---
created: 2026-02-03
tags: [meeting, weekly-sync, gco, aunz]
meeting_date: 2026-02-03
attendees: [TianaSmith, KarinSparring, MatthewBeltran]
meeting_type: weekly-sync
---

# GCO AU/NZ Weekly Sync - 2026-02-03

## Context
Weekly sync for AU/NZ GCO rollout team to discuss progress and blockers.

## Decisions
- **Exchange/Upgrade Solution**: Approved moving forward with Exchange/Upgrade solution for Q4 delivery. This unblocks scaling to 100%.

## Action Items
- [ ] Follow up with Quin about timeline @MatthewBeltran #2026-02-10 {{project:gco, priority:medium}}
- [ ] Update Confluence docs @KarinSparring #2026-02-07 {{project:gco}}

## Follow-ups / Open Questions
- Need to determine Booking Protect integration timeline
```

## Advanced Features

**Multi-source aggregation:**
If user provides multiple sources (e.g., Confluence page + their own notes), merge them intelligently.

**Recurring meeting detection:**
If meeting title matches pattern "X Weekly Sync" or "Daily Standup", suggest using previous meeting notes as template.

**Link to related items:**
Automatically link to Jira tickets if mentioned (e.g., "TMG-1393" becomes `[TMG-1393](https://jira.livenation.com/browse/TMG-1393)`)
