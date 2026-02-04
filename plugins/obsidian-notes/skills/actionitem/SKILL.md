---
name: actionitem
description: Quickly add an action item with owner, due date, and metadata that will appear in /whatamidoing
---

# Quick Action Item Capture

Add a new action item to your Quick Capture list with optional owner, due date, and metadata. These items will automatically appear when you run `/whatamidoing`.

## Vault Location
`/Users/matthew.beltran/Documents/Obsidian Vault`

## Capture File
`/Users/matthew.beltran/Documents/Obsidian Vault/Quick Capture.md`

## Action Item Format

**Simple format (backward compatible):**
```
/actionitem Review the new API documentation
```
Output: `- [ ] Review the new API documentation`

**Enhanced format with metadata:**
```
/actionitem Review API docs @TianaSmith #2026-02-10 {{project:gco, priority:high}}
```
Output: `- [ ] Review API docs @TianaSmith #2026-02-10 {{project:gco, priority:high}}`

**Format components:**
- `@owner` - Person responsible (e.g., @TianaSmith)
- `#YYYY-MM-DD` - Due date (e.g., #2026-02-10)
- `{{key:value}}` - Metadata tags (e.g., {{project:gco, priority:high}})

All components are optional and can be in any order after the task text.

## Instructions

1. **Parse the action item from user's command**:
   - Extract the base task text
   - Look for owner pattern: `@[A-Za-z]+`
   - Look for due date pattern: `#YYYY-MM-DD`
   - Look for metadata pattern: `{{key:value, key:value}}`
   - Example input: "Review API docs @TianaSmith #2026-02-10 {{project:gco}}"
   - Parsed:
     - Text: "Review API docs"
     - Owner: "@TianaSmith"
     - Due date: "#2026-02-10"
     - Metadata: "{{project:gco}}"

2. **Check if the capture file exists**:
   - Use Read tool to check if `Quick Capture.md` exists
   - If it doesn't exist, create it with proper YAML frontmatter

3. **Append the action item**:
   - Read the current contents of the file
   - Construct the full action item line with all parsed components
   - Format: `- [ ] <text> <@owner> <#due-date> <{{metadata}}>`
   - Use Edit tool to add the new item to the file
   - Add items under an "## Action Items" section

4. **File format** (if creating new):
   ```markdown
   ---
   created: YYYY-MM-DD
   tags: [quick-capture, action-items]
   ---

   # Quick Capture

   ## Action Items
   - [ ] <action item text>
   ```

5. **Response to user**:
   - Confirm the action item was added with all metadata
   - Keep the response brief
   - Example: "✓ Added: Review API docs @TianaSmith (due 2026-02-10)"

## Important Notes
- **BE FRICTIONLESS**: This skill should be as quick as possible
- **DO NOT ask about committing changes** - just add the item and confirm
- **DO NOT ask follow-up questions** unless the action item text is completely missing
- Support both simple and enhanced formats
- Always append to the "## Action Items" section
- Maintain the checkbox format: `- [ ] ` followed by the text and metadata
- Keep the response minimal - just confirm it was added
- If no action item text is provided, ask the user what they want to add

## Examples

**Input:** `/actionitem Review docs`
**Output:** `✓ Added: Review docs`

**Input:** `/actionitem Complete sign-off @TianaSmith #2026-02-10`
**Output:** `✓ Added: Complete sign-off @TianaSmith (due 2026-02-10)`

**Input:** `/actionitem Update Confluence @KarinSparring #2026-02-05 {{project:gco, priority:high}}`
**Output:** `✓ Added: Update Confluence @KarinSparring (due 2026-02-05, project:gco)`
